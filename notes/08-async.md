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

