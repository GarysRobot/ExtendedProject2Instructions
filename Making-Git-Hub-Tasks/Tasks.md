## Task 1.
For package structure use standard:
* views
    * This contains the html templates which are the pages that are viewable in the browser.
* controller
    * API endpoint entry
    * Responsible for displaying views files
    * Interacts with the service layer

Then make folders:
* service
    * Orchestration, should be lightweight seeing as we're only calling one endpoint
    * Service should contain all the logic and checks we want to happen. e.g. is the submitted data the correct format to be added into the database.
* connector
    * To send requests to external services (The GitHub API in this case)
* model
    * Domain model data representation
* repository
    * This contains the methods to interact with your database

Create your package structure with the corresponding files (e.g. controller class...).
Your mongodb should contain users which will have the following information: username, date account created, location, number of followers, number following.
Look at the return of a user from the GitHub API to help you make your model of a user. Try inputting your GitHub username into the url to see: https://api.github.com/users/{yourUsername}

Set up your mongodb database and a model of the user it will accept.
When adding users to the database make sure there cannot be duplicate usernames inside the database.

TO NOTE: When using the GitHub API you can come across rate limits. If this occurs it can be easier if upfront you use your own git credentials for authorisation - https://developer.github.com/v3/auth/#basic-authentication (you may not need to worry about authorisation yet and can come back to this once you get to task 9 as authorisation is needed when you start manipulating repositories on the GitHub API.)

## Task 2.
Create a route that will return a user from the GitHub API with the route:
{url}/github/users/{username}

When somebody accesses your app at the above url, you should display the user on a views page.
Use this connector to do this:
https://api.github.com/users/{username}

## Task 3.
Make routes for all the CRUD commands (Create Read Update Delete)

## Task 4.
Make a route and add other methods to add a user from the GitHub API to your repository.

## Task 5.
Make a  new route: /github/users/{userName}/repositories That will list the names of all public repositories for the provided username
Make use of the GitHub API: https://api.github.com/users/{username}/repos
Once this page exists, add a link “Repositories” to the page created in Task 2, so that as a website user you can navigate from somebodies profile to their list of repositories.

## Task 6.
Add a new route /github/users/:username/repos/:repoName
On this page display the names of files & folders (as determined by an API call) for the selected usernames’ repository.

## Task 7.
Make a new route GET /github/users/:username/repos/:repoName/*path
The path will be path to file I.E repoName/folderName/fileName.scala, you can base64 encode path for ease.
If the path given resolves to a file, display the plaintext of the file on the page.
If the path given is a folder, display the files & folder names (In the same way it's displayed in the first part of Task 5)

## Task 8.
Link up the pages. I.E the first step of task 5 doesn't only list the files/folders, but they are hyperlinks that will direct to the correct page in the  stretch exercise.
For example, /github/users/AprilGar/repos/ExtendedProject2Template, will show various files and folders including the folder "app". If you click "app" you  will be directed to:
/github/users/AprilGar/repos/ExtendedProject2Template/app

Do the same on the /*path pages, so that you can, from the top level of a repository, browse all folders and files.

## Task 9.
When it comes to unit testing your connector (the file using ws client that connects to the API) you can use wiremock to mock the API responses.

To use wiremock in your library dependencies in the build.sbt file add:
"com.github.tomakehurst" % "wiremock-jre8" % "2.33.2" % Test

If you run test if you get an error about jackson databind after adding the wiremock try adding this to your build.sbt file:
dependencyOverrides +="com.fasterxml.jackson.core" % "jackson-databind" % "2.11.0"

## Task 10.
Now try and add methods to get, create, update and delete files in a repository on the GitHub API (not on your database data).
Follow this link for instructions and work your way through each of the steps:
https://docs.github.com/en/rest/repos/contents?apiVersion=2022-11-28
You will need a personal access token to make changes in the API. This token should NOT be hardcoded into your code, as it should be for your eyes only. Try storing it as a permanent environment variable called AuthPassword, e.g. export AuthPassword= yourToken.
For details on how to create an access token see: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
Make curl requests in terminal for these routes and write tests to check they are all working.

## Task 11.
Now that you have accomplished step 10 instead of using curl requests in terminal try creating a form, so you can complete these routes from your browser.

## Task 12.
Now time to have some fun with the front end!
Add some css styling to the layout of your pages. For example you could change the font, change the layout of the text, add some colour, add a back button. How it looks is up to you. Get creative!
