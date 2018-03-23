# Getting Started with Azure Functions

**Azure Functions** is a solution for easily running small pieces of code, or "functions," in the cloud. You can write just the code you need for the problem at hand, without worrying about a whole application or the infrastructure to run it. Functions can make development even more productive, and you can use your development language of choice, such as C#, F#, Node.js, Python or PHP.
You can find out more about Functions online in the [Microsoft Azure subsite for  Functions](https://docs.microsoft.com/en-us/azure/azure-functions/).

In this lab, you will learn how to:

  * [Create a function from the portal quickstart](#create-from-portal)
  * [Create a function from the Command Line Interface (CLI)](#create-from-cli)


<a name="create-from-portal"></a>
## Create a Function from the portal Quickstart

1.	Sign in to the [Microsoft Azure portal](https://portal.azure.com/).
2.	In the Jumpbar, click **Create a resource +**, then select **Compute**, and scroll down for  **Function App**. 
    ![Screen shot 001 - New Azure Function App from the portal][1]
   
3. For the new Function app we have to define several values. 

    ![Screen shot 002 - Function creation values][2]

   1. **App Name:** The name of the function, this will become the resource url: *yourname*.azurewebsites.net
   2. **Subscription:** The desired subscription you want to run the function on.
   3. **Resource Group:** By default it will create a new resources group for you function. But you can also pick an existing one if you have one at hand.
   4. **Hosting Plan:** This part requires some attention as money is involved here:
        a. By default the Hosting Plan is set to **Consumption Plan**. This means that you *Pay-As-You-Go* so when the function requires limited resources it's fairly cheap. But if you manage to put your function in a loop you might be in for a surprise at the end of the month! So be carefull with this option. 
        b. The second option **App Service Plan** lets you select a predefined price based on predefined resources. This gives you some more 'security' over pricing. When you select 'App Service Plan as a Hosting Plan you can Create a New plan and select the location where you want your Function to run (around the globe that is) and select a desired Pricing Tier.
   5. **Storage Account:** Create or select an account where you want to store function data (and the function code)

4. When you've set all the variables click 'Create' in the bottom of the pane. The Function app will be created and deployed. This takes a moment. So grab some coffee or read a good book.

5.	Once the new *Function App* is created you need to create a new function. Click on the '+' sign next to Functions to open the 'Get started quickly screen'. 

6. Select the type of Function you want to run. For this simple quickstart Select *Webhook + API* followed by *C#* and then click *Create this function*
 ![Screen shot 003 - Select a type of function][3]

7. After the Function is created you get to see a dashboard with some code and a couple of buttons. Just press **Run** and see what happens.

8. In the right bottom corner you can see the output result. Obviously you can change the *name* request property in the request body and press *Run* in the bottom right corner to see the changes.
 ![Screen shote 004 - HTTP Result][4]

9. Now we have a functional 'API' so to speak. We need an URL to send requests to. In the top right corner there is small link **'</> Get function URL'** Click this link to gain the URL. 
 ![Screen shot 005 - API URL][5]

10. You can test this URL by just plain pasting it into the browser and run it. Additionally you can append a 'name' property into the querystring to test the response.
 ![Screen shot 006 - HTTP Response][6]


 There you have it. A simple, but working, Azure Function.

===========================
===========================
 

 
<a name="create-from-cli"></a>
## Create a function from the Command Line Interface (CLI)

In this Lab we will create the same Azure Function as before but we don't create it in the cloud via a fancy portal. We want to create it locally before sending it to Azure. 
This is convenient because this way we can develop and test the function without any Azure costs (as we are using our localhost IIS as 'provider')

1. First of, make sure you have Node Package Manager (NPM) installed. See [npmjs.org/get-npm](https://www.npmjs.com/get-npm) for more information.

2. Next, open the command prompt as administrator (you can use the nodejs command prompt or the default DOS prompt)  navigate to a desired empty folder and install the *azure-functions-core-tools* package globally:
    ```code
    npm install -g azure-functions-core-tools
    ```

    Which results in npm downloading and installing the _Azure Functions CLI_ package into the current directory.
    ![Screenshot 007 install Azure Functions CLI via NPM][7]

3. Meanwhile create a new folder on a location where you desire to create a new local Azure Function.

4. When the installation is done navigate via the prompt to the directory you just created.

5. Run *func* as a command to the see possible options.
![Screenshot 008 Create a new Azure Function via the CLI][8]

6. We want to create a new Azure Function so let's run the following commmand:
    ```code
    func new
    ```

7. It will return a list of language options. Use the **UP** and **DOWN** key to scroll trough the possible options and select **C#** by pressing *Enter*.

    ![Screenshot 009 A new function based on C#][9]

> Tip: Hit CTRL+C to abort the current execution (for instance when you picked the wrong template)

8. Next select the **HttpTrigger** option from the template list.
9. Finally type a name of your Azure Function and press enter to start the creation of the Function. Please be aware that the name you enter here will be created as a folder so try to prevent spaces and other non-folderish-names and keep it short.
![Screenshot 010 Naming the Azure function][10]

\
```<nerd-modus>```

You can also go rogue and type the whole command at once by using the following parameters:

        > func new -l C# -t HttpTrigger -n AzureBootcampLocal
![Screenshot 011 Be that nerd!][11]

```</nerd-modus>```


10. Now when you check out the directory you can see that a new folder was created, with the name you've just entered and a foursome of files. You can open run.csx and check out the code. That might look a bit familiar. That's because it's the same default template as we created in the online portal. 
11. Tryin to run this Azure Function with ```func run AzureBootcampLocal``` followed by an extra enter (confirming the launch of a new server) leads to an unforgiving and not-so-very-explanatory exception: **Unable to find function project root. Expecting to have host.json in function project root.**
![Screenshot 012 Wut?!][12]

12. Before you can run the function you need to initialize it first. You can do so by running the next command: ```func init```

  
13. After that you can run ```func run AzureBootcampLocal``` again to start up the local server and run your Function. Hit enter when the question appears of always showing a warning. This will open a new Command window showing the host information like below:
 
    ![Screenshot 013 Localhost][13]


14. Now open a random browser and navigate to the base address where your function is running: Meaning only the localhost and the assigned port. 
This will show up a page confirming that the server is operating and the function can be run.
![Screenshot 014 Localhost][14]

15. When you navigate to the full address you'll get the message like below:
![Screenshot 015 Localhost][15]

16. So append the requested parameter to the URI string and run request again. 
![Screenshot 016 Localhost][16]

> You can also use Postman instead of your browser.
![Screenshot 017 Request via Postman][17]


17. There you have it (again), A fully functional Azure Function, but local so you can test it first.



## Summary
By completing this lab you have learned how to get started with Azure Functions. 
For more information, please check out [functions.azure.com](https://functions.azure.com)

<!--Image references-->
[1]: media/001_Portal_New_Function.png
[2]: media/002_Portal_New_Function.png
[3]: media/003_Portal_New_Function.png
[4]: media/004_Portal_New_Function.png
[5]: media/005_Portal_New_Function.png
[6]: media/006_Portal_New_Function.png
[7]: media/007_CLI_New_Function.png
[8]: media/008_CLI_New_Function.png
[9]: media/009_CLI_New_Function.png
[10]: media/010_CLI_New_Function.png
[11]: media/011_CLI_New_Function.png
[12]: media/012_CLI_New_Function.png
[13]: media/013_CLI_New_Function.png
[14]: media/014_CLI_New_Function.png
[15]: media/015_CLI_New_Function.png
[16]: media/016_CLI_New_Function.png
[17]: media/017_CLI_New_Function.png
