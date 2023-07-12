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


#NOTE - Right now, in the main.js, comment out the DbConnection.connect as it connects to databases, and we will do that later. Do the same to the Auth0Provider in the startup.js unter the ConfigureMiddleWare function.

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

#STUB - Getting started
1. When making a new project, type bcw create > express-mvc. This allows us to load up a client, a server, and will allow us to use MongoDB to store information
2. Code . into your new project, and select open when prompted to open a new workspace. This will open a new, separate VSCode Folder
	- This will have a client and a server which have controllers, services, etc.
3. In the .env file, you will use the auth0 information to fill out your .env file in both the client (env.js) and the server (.env).
	- In the CONNECTION STRING, between the / and the ?, type in your project name so that it is easier to find in MongoDB
	- THIS SHOULD NOT BE PUBLIC. In the gitignore file, type in .env to prevent it from uploading to github.
	- You can copy and paste it somewhere safe so that you can just reuse it every time you need it. It will not change unless you change your domain and connection.
4. Then you will either hit the debug/run or the bcw serve and run both the client and server
	- When you create/sign in to your auth0 account, it will post the user information in both the auth0 and MongoDB database.
	- MongoDB will automatically create folders for our API if we set them up correctly

#STUB - Creating Schemas
- Schema stands for schematic and it tells MongoDB what is allowed to be stored in each folder. This is helpful for security and preventing malicious text or code from entering the database. #NOTE - ALWAYS CODE AS IF EVERYONE IS MALICIOUS AND EVERYONE IS STUPID. Code as if you are under attack and make sure that you cover your bases.
	- This also prevents users from using an application like Postman from going around your validation and protections on the front end. It protects the backend, too.
	- ORM: Object Relational Mapper; Mongoose is the ORM for our node model
	- Schemas have almost the exact same purpose as models

- To make a Schema: 
	1. Make a new model (like Car.js)
	2. Export the class
		export const CarSchema = new Schema( #NOTE - Schema will be imported from Mongoose
			make:{
				type: String, #NOTE - This can be any type of value (number, boolean, etc.)
				required: true #NOTE - This makes it so that we cannot submit a car if it doesn't have this property.
				maxlength: 50, #NOTE - This is the same kind of form validation that we would have in the front end, but now on the backend so that people cannot submit a bunch of malicious code.
				minlength: 3
			},
			model:{
				type: String,
				required: true,
				maxlength: 50,
				minlength: 1
			},
			year: {
				type: Number,
				required: true,
				max: 2025,
				min: 1901
			},
			color:{
				type: String,
				maxlength: 100,
			},
			ownedByGrandma:{
				type: Boolean,
				required: true,
				default: false #NOTE - This is if the user doesn't provide a value
			},
			miles:{
				type: Number,
				required: true,
				max: 1000000,
				min: 2
			},
			engineType:{
				type: String,
				enum: ['v8', 'v6', 'v7', 'v19', 'big', 'small', 'electric', 'check', 'medium'], #NOTE - Requires the submission to be one of the items in the enum.
				default: 'medium'
			},
			description:{
				type: String,
				maxlength: 500,
			},
			price:{
				type: Number,
				required: true,
				max: 1000000,
			},
			imgUrl:{
				type: String,
				required: true,
				default: '(some url)',
				maxlength: 1000
			},
			#REVIEW This is a really important object to have on your model!!! This will ensure that only the correct user can edit or delete objects on the webpage.
			creatorId:{
				type: Schema.Types.ObjectId, #NOTE - This is a schema that is created by MongoDB, so we can pull it from there. It provides the creatorId.
				required: true,
			#NOTE: When posting with postman, you can use the creatorId the you get off of your sample user account in MongoDB.
			}
		)

	3. If you copy in ({timestamps: true, toJSON:{virtuals:true}}) at the bottom your your export inside the parens, you will make it so that your model automatically gets a createdAt and updatedAt (timestamps) and it will automatically create an ID (virtuals)

	4. Go to DbContext.js to register your new collection
		Cars = mongoose.model('Car', CarSchema) #NOTE - Your model name should be plural because multiple things are being stored inside it, with the singular name and schema that it is being pulled from inside the parens.

#SECTION - Making a Controller inside of the Workspace

- This is almost the same as setting it up in Node, as above:
	export class CarsController extends BaseController{
		constructor(){
			super('api/cars')
			this.router
			.get('', this.getCars)
		}

		async getCars(req, res, next){
			try{

			} catch(error){
				next(error)
			}
		}
	}

#SECTION - Making a Service inside of the Workspace

- This is also almost the same as setting this up in Node, with some important changes

	class CarsService{
		async getCars(){

			const cars = await dbContext.Cars.find() 
			
			#NOTE - Remember to use async/await in order to make sure there is time to pull down this information. Then, pull the Schema out of dbContext. After that, we are using the MONGOOSE method find. This is NOT the same as the array method of find. 

			#REVIEW - MongoDB doesn't store our code as Javascript or JSON. Mongoose translates it from BSON (binary script) into JSON. It is the translator that stands between us and the database, and is an ORM.

			return cars
		}
	}
	export const carsService = new CarsService()

#SECTION - Creating an item in our database

- As before, under this.router create a post method in the constructor
	.post('', this.createCar)


	async createCar(req, res, next){
		try{
			const carData = req.body

			const car = await carsService.createCar(carData)

			res.send(car)
		} catch(error){
			next(error)
		}
	}

- In the service:
	async createCar(carData){
		const car = await dbContext.Cars.create(carData) 
		
		#NOTE - Mongoose will take the carData, convert it so that MongoDB can store it, and then return that information back to us in the return below.

		return car
	}

#SECTION - Securing your server with Middleware

- In the constructor, you will use a .use method
	.use(Auth0Provider.getAuthorizedUserInfo) #NOTE - in this case, Auth0Provider is the middleware that requires authorization before the rest of the CRUD methods can be used that should be attached to a user.

	#NOTE - Any thing that comes after this .use method, you will HAVE to be logged in via Auth0 in order to use. Otherwise, you will throw a 401 error.

- In Postman, go to the Authorization tab. Change your Authorization Type to Bearer Token, then paste the Bearer token from your ⚙️token in the headers from the client login on localhost:8080 here (Check the Network tab > Preview tab in the Dev Tools). This acts like logging into the website, with secure information. Keep in mind that they do have a timeout, which you can change, or you can re-login to get a new one.

- In your previous code which accesses accounts (post, put, delete), in the controller after your const carData = req.body

	carData.creatorId = req.userInfo.id

	#NOTE - This attaches the creatorId to the request so that a malicious user can no longer use their bearer token to post to someone else's account. This works because in the controller, we are using the .use method. They can still post like they want to, but it adds their own bearer token and creatorId so they add those posts with their own name.

	#NOTE - If there is no data, you can instead use const userId = req.userInfo.id and then pass it into the service as a secondary parameter.

#SECTION - Relationships
- UML - Unified Modelling Language. Points from one data type to many or one other to define their relationship with each other.

- Objects can point toward one or more other objects that are related to each other. These would be like pages that belong to a book, which is a One to Many relationship.
	- The items that belong to the other item would have a property on them that defines which thing they belong to with an id.
	- EXAMPLE: #NOTE Not codeable script 
		book[
			id:{objectId},
			title: {string(100)},
			description:{string(500)},
		],
		page[
			id: {objectId},
			chapterNum: {number},
			content: {string(100)},
			bookId: {objectId}
		],
		account(author)[
			id: {objectId},
			name: {string100},
			picture: {string(500)},
			email: {string(100)}
		],
		bookAuthor[ #NOTE This type of object will make sure that we can have multiple items stored on another object without an array, which would need a for loop and would get messy. It makes many-to-many objects easier to access, in addition to making the properties on them easier to access.
			id: {objectId},
			bookId: {objectId},
			authorId: {objectId}
		]

#STUB - Getting Started:
	(MAKE SURE YOUR ENV IS SET UP)
	1. Make your models first based off of the UML
	2. Set up your controllers and services. You will have one for each model. => in the controller, make sure you have a .use function and your super.
		- In the "Many" object in the one-to-many relationship, in your model you will write:
		
		export const PageSchema = new Schema({
			chapterNumber:{ type: Number, required: true, min:0},
			content:{type: String, required: true, maxlength: 1000},
			bookId: {type: Schema.Types.ObjectId, required: true, ref:'Book'}, #REVIEW: This will be an id that is set up the same way as an individual item. However, the reference is to the Book schema, which has been named 'Book'.
		})

			- In its service: 
				- You will set up the controller and service the same way EXCEPT when writing a method in the service. In this case, you will likely call in another service in order to pull off the many's from the one. For example, you would connect the book and pages services so that you can use a getBookById method to find the pages that are attached to that id.

#SECTION - Writing a virtual
- This will be used in Many-to-Many objects, like in the books to authors example below. This will be used to grab collections inside of other objects.

1. Inside your model, after your properties, write:

	BookAuthorSchema.virtual('book', { #NOTE This is the name of the virtual, it only works if the schema has that property on it.
		localField: 'bookId', #NOTE Refer to this property on this object

		foreignField: '_id',

		justOne: true #NOTE There is just one of these things

		ref: 'Book' #NOTE Reference the book schema

	})

2. In the service, in one of the CRUD functions:

	await bookAuthor.populate('book') #NOTE This will run all the virtuals on this property.

> Another example:
	BookAuthorSchema.virtual('author', {
		localField: 'authorId',
		foreignField: '_id',
		justOne: true,
		ref: 'Account'
	})

	- In the service:
		await bookAuthor.populate('author', 'name picture') #NOTE this is in Mongoose syntax

