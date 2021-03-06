# Create a new project (.NET Framework)

Go to menu **File** >> **New** >> **Project** and select **Web** >> **ASP.NET Web Application**. For this sample, let's name it **forgesample**. On the next dialog, select **Empty** and select **Web API**. 

Install the Autodesk Forge NuGet package: right-click on the project (**Solution Explorer**), select **Manage NuGet Package**, then on **Browse** search for **Autodesk Forge** and install it our **forgesample**. 

![](_media/net/create_project_webapi.gif) 

!> If **Web** & **ASP.NET** project types are not available, please review [Tools](environment/tools/net) section

## Web.Config

On the **Web.Config** file, add the Forge Client ID & Secret entries (obtained when you created your app). By default, it should already have a `<appSettings></appSettings>` after `<configuration>` and before `<system.web>`, adjust as shown below:

```xml
....
<configuration> <!-- this line is already on your file -->
  <appSettings>
    <add key="FORGE_CLIENT_ID" value="Your client ID here" />
    <add key="FORGE_CLIENT_SECRET" value="Your client secret here" />
    <add key="FORGE_CALLBACK_URL" value="http://localhost:3000/api/forge/callback/oauth" />
  </appSettings>
  <system.web> <!-- this line is already on your file -->
....
```

The ASP.NET engine limits the size of file on uploads to 4Mb and filter requests bigger than 30Mb. We can change this limit to the maximum (or you can adjust to your needs). On the `web.config` file, search for `httpRuntime` and add the `maxRequestLength` to it, as shown below:

```xml
<!-- httpRuntime targetFramework is already on your file, just add the maxRequestLength -->
<httpRuntime targetFramework="4.6.1" maxRequestLength="2097151" />
```

And add the **security** >> **requestFiltering** limit:

```xml
  </handlers> <!-- this line is already on your file -->
  <security>
    <requestFiltering>
      <requestLimits maxAllowedContentLength="4294967295" />
    </requestFiltering>
  </security>
</system.webServer> <!-- this line is already on your file -->
```

Learn more about [maxRequestLength](https://msdn.microsoft.com/en-us/library/system.web.configuration.httpruntimesection.maxrequestlength.aspx) and [maxAllowedContentLength](https://msdn.microsoft.com/en-us/library/ms689462.aspx). 

## Port

Last, to make your app consistent with all other **Autodesk Forge** samples, let's change the port to **3000**: go to project **Properties** (right-click on project name), under **Web** tab, then change the **Project URL** to `http://localhost:3000`.

![](_media/net/port.png) 