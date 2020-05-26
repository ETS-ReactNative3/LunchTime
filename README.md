
## Preview
<img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/homescreen.jpg" width="140"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/capturescreen.jpg" width="140"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/camerascreen.jpg" width="140"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/analyzescreen.jpg" width="140"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/recscreen.jpg" width="140"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/recipescreen.jpg" width="140">

# Lunchtime
## The Problem
During the COVID-19 pandemic, millions of people around the world are spending an unprecedented amount of time at home. One major consequence of being unable to leave the house is the need to cook every single meal. Furthermore, many have lost gym and/or outdoor access and are unable to exercise. Given the circumstances, it can be difficult to ensure you are eating a healthy, balanced diet each day. Especially in such a high-stress situation, people don't want to spend hours cataloging their food intake and googling new recipes. We built LunchTime to take care of all of these problems in a fast and effective way.

## Our Solution
LunchTime helps you keep track of what you eat and recommends new, healthy recipes specifically catered to your tastes and dietary needs, all within seconds.

**Capture** LunchTime leverages computer vision technology from Clarifai and nutritional data from Wolfram Alpha to get all the important information about your meal (key ingredients, calories, protein content, etc.) from an image. All you have to do is open up LunchTime, take a photo in the app, and you're done! All the information about your meal is stored safely in our database and you can look back on it whenever you like.

**Record** In the "Home" tab, LunchTime keeps a running tally of your nutritional intake for the day. Whenever you're debating whether it's a good idea to squeeze in that extra snack, LunchTime is there for you with specific information on how many calories you've eaten that day along with loads of other helpful statistics including fiber intake, fat consumption, and more.

**Predict** Whenever you're tired of searching the web for something yummy to eat that satisfies your dietary needs, just head over to the "Recommendations" tab in the app. Our algorithms will then look through your entire meal history and pick out the ingredients you liked in the past. We then search Tasty for recipes with similar but slightly different ingredients to help you change things up when you're bored of the same food every day while also ensuring the new recipe will be something you'll enjoy. Finally, we check how much more protein, fat, and fiber you should have that day to fulfill a 2000 calorie, well-balanced diet, and select the recipe that best fulfills your nutritional needs. Without any work on your part, these suggested recipes will appear in the "Recommendations" tab of the app along with recommendations on how many servings of the recipe you should make to maintain a healthy diet.

## Technology
Frontend The frontend was built in react-native for optimal cross-platform use and an elegant user interface.

APIs Whenever a user submits an image in the app, it immediately sends the image to the Clarifai API (https://www.clarifai.com/models/food-image-recognition-model-bd367be194cf45149e75f01d59f77ba7), which returns a list of ingredients for the meal depicted in the image. We then pass this data on to the Wolfram Alpha API (https://www.wolframalpha.com/examples/society-and-culture/food-and-nutrition/) which returns the nutritional value of each ingredient in the meal. The app then sends the ingredient list and nutrition information to the Firestore database.

Database To store user meals and nutritional data, we used Firebase's Firestore NoSQL database. For each user, we keep a running log of the ingredients in every meal they have eaten, enabling the prediction API to infer what foods a given user will like. We also store the user's present and past nutritional data. Whenever the user goes to the "Record" tab in the app, the database sends the present day's nutritional values, which are automatically updated whenever the user takes a picture of another meal in the app.

Predict API The Predict API receives a user ID as input and returns a link to a Tasty (https://tasty.co) recipe, a number representing how many servings of that recipe the user should make, and a link to an image of the food in the recipe. After receiving the user ID, the API pulls the user's entire meal history and present nutritional information from the database. It then encodes a random subset of the user's past ingredients as GLoVe embeddings and randomly samples three words with similar embeddings to the ingredients. These three terms are then passed as a query to the Tasty API, which returns a list of 40 potential recipes the user could make and their respective nutritional contents. Our API compares the user's food intake for that day to an ideal 2000 calorie diet and calculates the ratios of protein, fiber, and fat relative to calories that the user should consume in their next meal. By comparing these ratios to the same ratios for each recipe, we obtain the recipe most suited to the dietary needs of the user. Ultimately, we compare the total calories the user should consume to reach the 2000 calorie goal and the calories in one serving of the recipe to calculate the total number of servings the user should make of the given recipe. The recipe, serving number, and image link are all returned to the app when a user goes to the "Predict" tab.

## Challenges
Despite building a very frontend-heavy application, we only had one team member fluent in react-native, which put a bottleneck on our progress in some areas. It was also difficult to make all the connections between the frontend, database, and prediction API work smoothly. We were generally successful getting each component to work, but spent much more time than expected on implementing the many API calls and database queries. We had particular difficulty with the Clarifai API since it had rather poor documentation and required a complex procedure to submit valid requests.

## Next Steps
With our trove of dietary data, there are many ways we could expand LunchTime's functionality. Firstly, we could further personalize the app by allowing each user to select their own dietary goals, or even recommending dietary goals given the user's past eating habits, weight, height, gender, and other personal data. We could also add a feature allowing more involved users to catalog their eating habits manually to ensure the greatest possible accuracy when recording food intake. Finally, we could add push notifications reminding users to eat, exercise, drink water, or perform other activities to keep themselves healthy every day.

### Built With
React-Native, Redux, Clarifai API, WolframAlpha API, Python, Firebase, Firestore, Gensim, Tasty

Our API: https://lunchtime-929c6.firebaseapp.com/

## Screens
<img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/homescreen.jpg" width="300"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/capturescreen.jpg" width="300"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/camerascreen.jpg" width="300"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/analyzescreen.jpg" width="300"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/recscreen.jpg" width="300"> <img src="https://github.com/ZovcIfzm/LunchTime/blob/master/readme-imgs/recipescreen.jpg" width="300">
