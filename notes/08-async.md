# Async

#SECTION - Getting Started

1. Create a controller like you normally would. Create a controller and hook it up to the router. 

2. Create a getDATA(){} function in your CONTROLLER 

3. Put a try/catch evaluator in your getDATA function. This allows mistakes to be caught as soon as they happen.
    EXAMPLE: 
    getMonsters(name){
        try{
            if(!name){
                throw new Error("No Name Supplied") #NOTE: throws act like returns here.
            }
            Pop.success(`${name} was supplied`)
        } catch (error){
            console.error(error)
            Pop.error(error.message)
        }
    }

4. Use this.getDATA() in order to use the data in constructor, as they are both being used in the same place.

5. Create and hook up your service.

6. Hook up your getDATA function in your service
    getMonsters(name){
        try{
            monstersService.getMonsters()
            Pop.success("We got the monsters!")
            }
            Pop.success(`${name} was supplied`)
        } catch (error){
            console.error(error)
            Pop.error(error.message)
        }

#REVIEW - Move on to step 8! Step 7 is good review for why things work the way they do in the link in step 8.
7. Create your request for info in the service #NOTE - JS doesn't like to wait for information to get caught and loaded. We need to make our get function an async/await function so that the server has time to send down the information (fulfill the promise) before JS moves on. 
    **async** getMonsters(){ 
        const response = **await** fetch(API URL)
        const jsonData = await response.json() #NOTE - the data isn't stored as readable JSON data, so we have to convert it to JSON. This also takes time, hence await.
        console.log(jsonData)
    }

8. Add a script tag to the bottom of your HTML body to take in axios, which will convert any data taken in from the API as readable data. As a result, step 7 is unnecessary. 

9. Create an AxiosService. #NOTE - You will likely need to create a different export function for each API Library that you use.

10. In the AxiosService write export const zeldaApi = axios.create({
    baseURL: '(Paste API Reference URL)'
    timeout: 8000 (If the API request takes more than 8 seconds, throw an error. 8 seconds is REALLY LONG for a user, so it doesn't really need to be longer than this.)
})

11. Back in the service, write:
        **async** getMonsters(){
            const resonse = **await** zeldaApi.get() (zeldaApi is taken from the AxiosService we made in steps 9 and 10)
            console.log(response) 

            #NOTE: this console log will give us an HTTP response code. If we have Status 200 in there, that means that the request and response were both good. If the response code is 404, that means that the data we requested is invalid and not found (for example, if the URL is misspelled or bad). We can see these specifically in the Dev Tools by going to the Network and filtering by Fetch/XHR to see the specifics of each status code returned, particularly when they throw an error.

            #NOTE: A 405 error will be that the CRUD method we used wasn't allowed. For example, using POST instead of GET.

            #REVIEW Always create a response console log so that you know what data you're getting and how it's being formatted. You can drill into it with dot notation to get the specific thing that you want out of the data.
        }

12. Make the same function in the CONTROLLER async/await, so that the controller doesn't move on without the service.
        async getMonsters(name){
        try{
            await monstersService.getMonsters()
            Pop.success("We got the monsters!")
        } catch (error){
            console.error(error)
            Pop.error(error.message)
        }
    }

13. You can pass the category in the params for the information that you specifically want to pull from the API. 

14. Create a model for the objects that you want to pull from the API.

15. Create the constructor for your data that you are pulling from the API. You can copy and paste it into the model and change the specific this getter for each specific object that's being passed through.
    - If they passed through the information in a different case (ex: snake_case)
    this.commonLocations = data.common_locations #NOTE: This still takes in the data, and because of the way that we called the information with this, we were able to change it back into a friendlier case.
    - You can create a this.id that takes in the ALREADY GENERATED id from the API
        this.id = data.id
    - You can also take in the image (again, check your console log to see if they are present and how the property was named.) with this.imgUrl = data.image

16. Create an object in the AppState to store the data you are pulling from the API
    monsters = []

17. Instantiate your passed data with the "new" method in the service. Use the MAP array method for this.
    EXAMPLE:
    const arrayOfMonsters = response.data.data.map(monsterPojo => new Monster(monsterPojo))  
    #NOTE: you will need to drill into the data you want in order to map it. This "data" is nested twice, hence why it is called twice.

    console.log(arrayOfMonsters)

18. Save your new array in the AppState
    AppState.monsters = arrayOfMonsters

19. Draw your data! This _will not_ be called in the constructor WITHOUT A LISTENER, because the data won't exist yet on page load. It has to think first. Make sure you have also made a template in the model for the draw function to use.

# NOTE: Best order to pull data from an API?

1. Create a model
2. Create a place in the AppState to store it.
3. Create a controller for that model.
4. Create a server to process the data coming from the API.

OR

1. Create a controller
2. Create a server to process the data coming from the API
3. Create a model.
4. Create a place in the AppState to store it.

#SECTION - Making a folder with MVC Auth

1. bcw create
2. mvc-auth
3. Enter your project name
4. no Git repo
5. cd into your project
**NEW** Items have been moved around and id's have also been added called 'auth-template', we also have script tags for auth0 and axios. DON'T take out any of the script tags! A new app.js file is env (environment).js. An AxiosService.js has also already been made. The baseURL in Axios is imported with env, DON'T change the premade axios instance name, as other functions within the premade template depend on it. 
6. Grab a baseURL from your API. Only grab the API without the filtered data types attached. We can attach those specific parts with concatting on get requests.
7. Put it in the env in export const baseURL = dev ? 'YOURURL' : 'DON'T WORRY ABOUT THIS PIECE RIGHT NOW1'

#SECTION - Using the MVC model in MVC Auth _some review, some new_
1. Create your Controller like normal, and ensure its connection with a console log in the controller
2. Hook up the Controller to the Router like normal.
3. Create a new view in the Router if necessary, use the premade About view as a reference for the syntax.
4. In the Controller, create your async get function. A "GET" function is the R for Read part of the CRUD acronym.
5. Write a try/catch statement inside the GET function, remember that this is so that the function has strict error handling.
6. In the try section of the try/catch statement, call the service with an await (EX: await carsService.getCar())
7. Create a const reponse/ const res (short for response)
8. Call the axios instance with api
    EX:
    async getCars(){
        const res = await api.get('specific URL from filtered request in API link')
        console.long(res) #NOTE always console long your information to see how it is being stored and which properties you need to drill into. Most of the time your drill is response.data, with .something after that changes depedning on the API.
    }
9. Make your model. You can copy one of the objects from your response in the previous step in order to make your model-making process easier.
    - Most of the models from the CodeWorks premade API has an ID on it. This ID will be used to make CHANGES on the car in the API using a CRUD method.
    - There will likely be two ID's, one with an underscore and one without. Use the one without the underscore in order to make your model 
      (this.id = data.id, not data._id)
		- Keep the creatorId from the data, as this will matter if someone wants to edit or delete and item that they made without someoen else interfering with it. It it's within an array, you can still use it with this.ARRAY = data.ARRAY
		- Some properties might be useless for your purposes. They do not need to be included in the model, based on your discretion.
10. Create an instance for your model in the AppState
11. Use the MAP method in your async/get/await in order to turn the Plain Old Javascript Objecs (POJO's) into useable data. In the CodeWorks API, the res.data is not nested any further, so you don't need to continue drilling down. Instead, start mapping that data with res.data.map()
	const builtCars = res.data.map(pojo => new Car(pojo))
12. Save your new data into the AppState with AppState.cars = built cars
13. Put a listener in your console to draw/log the cars (ARRAY of data, whatever it may be) as soon as they are built.

#SECTION - Create an item and push it up to the API (NOT STORING IT TO LOCAL STORAGE!)
1. Create a form for the user to submit data with. Make sure that the input areas match the data that is able to be submitted to the API.
2. In your controller, create a new async/await function which takes in the form event AND prevents refresh. This should still be inside a try/catch section.
	EXAMPLE: 
		async createCar(event){
			try{
				event.preventDefault()

				const form = event.target

				const carData = getFormData(form)

				console.log(carData) #NOTE always make sure your data looks good before you send it down to the service.

				await carsService.createCar(carData)

			}
			catch(error){
				console.log(error)
				Pop.error(error.message)
			}
		}
3. In the service, things are going to look different!
	 EXAMPLE:
		async createCar(carData){
			const res = await api.post('api/cars', {object}) 
			#REVIEW - BECAUSE WE ARE _CREATING_ DATA, WE ARE USING A POST REQUEST. We are also creating a body (PAYLOAD) inside the API category of cars, which is why we are grabbing the body that we want to put the object in, and the object itself.

			console.log("Created data??", {object})

		}
		#REVIEW - HOWEVER this will not work unless we have a creatorId, as this is part of the "required" form submissions in the API. That is something we can make up using the Auth0 Settings card at the top of the BCW API.

4. Plug in the domain, audience, and clientId into the env from the BCW API Sandbox to make it possible to submit data into the API. This will also create a Log In link in the navbar in your page. For testing purposes, you can make a fake account with a fake email (no connection to Google required). You can create a TempMail email as well.

5. If you try to create and post data and you get a 401 error, you need to log in (make it functional with step 4). If you get a 400 error, it means that you can post data but something happened along the way. Check the Network tab in your Dev tools, check the Preview tab in there, and then read the error for the specifics on the error. It might tell you what you are missing on your object that you need for your object to be accepted. Check your model!

6. When you are able to get a 200 OK HTTP Response, make sure that your API auto-refreshes so that your new object can get drawn to the page as soon as it is made.
	- Start by saving the object in your AppState in your function (step 3) with const builtCar = new Car(res.data) #NOTE - MAP is not required for this because we do not have an array of objects. We only have ONE, so MAP is not used on this because it is an array method, and we are submitting an object.
	- Push the new car into the AppState with AppState.cars.push(builtCar)
	- Make an emit!

#SECTION - To Delete an Item from the API
1. Make sure that there is a button on the model to click "Delete" on.
	- Give it an onclick that passes down the id of the item ('${this.id}')
	- Make sure that only the people who created the item can see the delete button.
	EXAMPLE
	get ComputeDeleteButton(){
		if(!AppState.account || AppState.account.id != this.creatorId){ 
			#NOTE this is an important check so that people who aren't logged in aren't able to see the delete button, and people who are logged into a different account can't see delete buttons on items they have not created. Attach a listener on accounts in order to make sure that the delete button is drawn when an account is chosen. The items will be drawn on page load BEFORE the account, so we need to have a listener on the accounts so that we can redraw them once it is found.
		return ``
		}
			return `button html here`
	}

2. Since this is also talking with an API, make sure it is also async/await in the Console.
	EXAMPLE 
	async deleteCar(carId){
		try{
			await carsService.deleteCar(carId)
		}
		catch{
			console.log(error)
			Pop.error(error.message)
		}
	}
3. Create the delete function in the Service
4. Put the Id of the object into the Delete request (similar to a URL in the Get request) so that it pulls up just that object in the API.
	- async deleteCar(carId){
		const res = await api.delete(api/cars/${this.carId}) #NOTE the delete() is a delete request to the api. The delete request will not have a body.
		console.log('deleted car', car.data) #NOTE car.data/res.data will return 'deleted value'
	}
5. Make sure to create a confirmation message for deletion!! Check Gregslist for a reference.
6. Create a splice method in the delete function in the Service in order to get the item out of your AppState, then emit.
	const carIndex = AppState.cars.findIndex(car => car.id == carId)
	if(carIndex == -1){
		throw new Error(`No car Index found with the Id of ${carId}`) 
		#NOTE this is an important step because if the index you are looking for doesn't exist, it will return -1. Then, if you use splice, it will take out the last item in an array which is BAD.
	}
	AppState.cars.splice(carIndex, 1)
	AppState.emit('cars')

#SECTION - Edit Items in the API
1. 

#SECTION - Facts

- Any request made to an API will always be an asynchronous request.

- We use URL's in order to make requests to get data.

- We use a GET request to request this data.

- The API's store their objects in JSON strings (JAVA SCRIPT OBJECT NOTATION)

- API's will pretty much always store their information as class objects.
    - They will also store these objects in categories, which will change the URL and make it easier to find the information you need/want.

- CRUD (Create, Read, Update, Delete) Requests are requests like GET, PUT, DELETE/DESTROY, or POST. Each one of these requests do something different in the CRUD acronym.

- We really won't change properties on an object that we are pulling from an API. We just take their data, build our model around it, and then format our website around that.

- We could change the properties on our locally stored data, if we really wanted to.

- Our MVC document is going to be basically the same, the only thing that will change is where we are getting our data from.

- Create Pop success/errors frequently and thoughtfully to notify your users when something goes wrong. This is good practice that we might not think about.

#SECTION - Syntax

