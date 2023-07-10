# Node

#SECTION - Getting Started
1. In the controller, type in bcw create > node-server-auth0
2. When spinning up the server, we will be using localhost:3000 instead of 8080. This is because we're using a server and API and want this to be on a separate server. You will use the RUN/DEBUG tab in VSCODE for this. In addition to refreshing the page, we will also click the respin button so that it runs and makes new requests from our API with a fresh and up to date server.
3. When making a controller, inside the constructor we will need to use a supercall which will calls the constructor on the basecontroller into the new controller.

    export class CatsController extends BaseController{
        constructor(){

            super('api/cats') #NOTE This is the "mount" which is a URL that we are using for our request. The "mount" is a parameter set in the base controller. It will likely match the type of data we want from the API.

            this.router #NOTE This connects to the router from Express so that we can accept requests from the client.

            .get('', this.getCats) #NOTE This is a method provided by node, which provides the same functionality as one of our CRUD methods. This is technically connected to the router, but is spaced down to make it more readable.
        }
    }

    async getCats(req, res, next){ #NOTE Every method that we make inside the controller that makes a CRUD request will take in these three parameters. Next is what runs when we throw an error, it is the default error handling with try/catches.

			try{

				const cats = await catsService.getCats() #NOTE This is sort of the same as making requests via the service like we normally would. We are just storing the data to send the response like below.

				res.send(cats)

				#REVIEW - Neither of this methods are preferred. They are good examples on how databases and requests owrk in node, but are not safe or standard.
					<!-- res.send('You made a request!') #NOTE whenever a request is made, we will be SENDING back a RESPONSE. -->
					<!-- res.send(cats) #NOTE This is an object class that was made in a new database in the db folder -->

			} catch(error){
					next(error)
			}
    }

4. To set up the service:
	class CatsService{
		getCats(){
			return cats #NOTE This would import the object class "cats" that we made in the database.
		}
	}

5. To make a request about ONE THING:
	- in the constructor of the controller via the this.router:
		.get('/:id', this.getCatById) #NOTE The slash colon is appended onto the super(url) and the colon is the id that is provided by the user. The colon is not shown in the url, it just adds something on to the url.

		async getCatById(req, res, next){
			try{

				const catId = req.params.id #NOTE In the params.id, this defines what is passed inside the parameters inside the .get in the constructor. The .id, or whatever the get is requesting, must be the same here as it is in the constructor.

				const cat = await catsService.getCatbyId(catId)
				
				res.send(cat)

				<!-- const request = req #NOTE console.log isn't really used in Node. Instead, put in breakpoints via the run/debug tab and you'll be able to see what is being sent up or sent back on a specific line. You can take these debugs out when you're done debugging. -->

				<!-- res.send('get cat by Id') #REVIEW again, this isn't standard, but is a great test to make sure that our response is working appropriately. -->
			}catche(error){
				next(error)
			}
		} 

	- in the service, we will write our typical find method:
		getCatById(catId){
			const foundCat = cats.find(c => c.id == catId)

			if(!foundCat){
				throw new BadRequest(`${catId} was not a valid ID`) #NOTE This is the same as throw new Error, but it just specifies which error (400 in this case) to throw.
			}

			return foundCat
		}

6. To post a new object in the API:
	- In the constructor after the this.router, write:
		-post('', this.createCat)

	- async createCat(req, res, next){ #NOTE The order does matter here for the params.
		try{
			const catData = req.body #NOTE this is like sending up the data, but we use res.body instead

			const cat = await catsService.createCat(catData)

			res.send(catData)
		} catch(error){
			next(error)
		}
	} 

	- In the service:

	createCat(catData){
		catData.id = cats.length + 1 (This is creating a new ID without the generate Id method.)

		cats.push(catData)

		return catData

	}

7. To delete something from the database:
	- In the constructor, after the router:
	.delete('/catId', this.removeCat)

	- In the Controller:
	removeCat(req, res, next){
		try{
			const catId = req.params.catId

			await catsService.removeCat(catId)

			res.send('Cat was send to the farm')
		} catch (error){
			next(error)
		}
	}

	- In the Service:
	removeCat(catId){
		const foundIndex = cats.findIndex(c => cat.id == catId)

		if(foundIndex == -1){
			throw new BadRequest(`${catId} was not a valid ID`)
		}

		cats.splice(foundIndex, 1)

	}


#NOTE - Right now, in the main.js, comment out the DbConnection.connect as it connects to databases, and we will do that later. D that same to the Auth0Provider in the startup.js unter the ConfigureMiddleWare function.

#SECTION - The tour of node
- In the client folder, you will see your index.html folder
- You will see an env file with environment variables that will be familiar due to the MVC pattern.
- In the server, you will see main.js. It is relatively small. You might need to comment out the DbContext.connect line of code. You will not need to interact with it much, it just adds middleware.
- The ConfigureGlobalMiddleware statif function is meant to be what the user might interact with throughout the application. It makes information available to git, localhost, etc 
    - helmet is a line of code that is meant to take out malicious or incorrect code. 
    - bp.json means that all parts of the body are JSON code.
- Controllers and services are still present like in the MVC design pattern.
- You will also have a Startup.js file which creates hallways for the router, which connect all controllers (doors in the hallway) to the router
- In package.json, the @bcwdev/auth0provider is the authenticator that ensures that only users with the correct ID are able to make requests on their content on a website.


#SECTION - Controllers in Node
- The BaseController registers your other controllers so that they can be sent in the hallway to the router
- The ValuesController is an extension of the BaseController which allows controllers to be connected more easily. It's also a good reference if you forget anything about setting up and using Controllers.
    - When we use extends, we are taking in the information from the BaseController that we will need to make a new controller work. We will need to write extends on every controller that we make.
- They will typically be the first thing that you set up when you make your server.
- You do not need to hook up controllers, because this is set up for us in the Startup.js


#SECTION - Postman
- Mocks having a client sent out, and creates data to get, post, put, delete for you so that you can test your code more effectively.

- You will create a new collection for each project, to keep the information a little bit more organized.
- You can then click on the drop down to choose the HTTP request that you want, if you provide the correct URL.

- To POST, you will go to the Body tab under the URL, then select JSON for the body type. After that, you can send up a new object.

#SECTION - MongoDB
- This is a database which holds and handles all of our data.
- You need to make a free account in order to use it.
- For this purpose, you can make your Project Name CodeWorks Classroom.
- A cluster is the collection of your databases.
- When you add a new Database User, don't make your username and password the same as what it is for the overhead account.
- You need to add the IP address of your location that the database will be used in. It's easier to select "Allow Access from Anywhere" instead of adding your IP address every time you move your computer to a new location.
- When you connect, you will need to copy and paste the connection string with the correct password into the .env file with the connection string inside it, without quotes.

#SECTION - Models/Schemas
- ORM: Object Relational Mapper; Mongoose is the ORM for our node model
- Schemas have almost the exact same purpose as models
- 

#SECTION - Facts

