# ZAPROXY
OWASP ZAPROXY Tutorial
ZAP PROXY TUTORIALS (YouTube: Arkenstone Learning: OWASP ZAP Step-by-Step)
//-------------------------------------------------------------------------------------------------------------------------------
//-------------------------------------------------------------------------------------------------------------------------------
TABLE OF CONTENTS
1.	Introduction	
2.	Main feature	
3.	Installing ZAP & Understanding its features	
4.	Creating Dynamic SSL Certificate & Importing in Browser	
5.	Proxy Web Traffic through ZAP	
6.	Configure FoxyProxy	
7.	Installing Mutillidae	
8.	Intercepting request with ZAP (Man in the Middle Attack-MITM)	
9.	Intercepting specific request with ZAP	
10.	Manually explore for Vuln Assessment in ZAP	
11.	Spidering a Website with OWASP	
12.	Automated Vuln Assessment of a Single Page in ZAP	
13.	Automated Vuln Assessment of Entire Site in ZAP	
14.	Automated Vuln Assessment of a Partial Site in ZAP	
15.	Generating Vuln Assessment Report in ZAP	
16.	Contexts, scope and Modes in ZAP	
17.	Sessions in ZAP (first screen pop in start)	
18.	ZAP Request Editor	
19.	Passive Scan Rules in ZAP	
20.	Active Scanning in ZAP	
21.	ZAP Scan Policy	
22.	Attack Mode	
//-------------------------------------------------------------------------------------------------------------------------------

ZAP TUTORIALS
1.	Introduction
    a.	Open source, Web Application Testing Tool
    b.	Cross platform: Win, Mac & Linux
    c.	Can be used for Automated Testing
    d.	Can be used with Burp Suite
//-------------------------------------------------------------------------------------------------------------------------------
2.	Main feature
    a.	Intercepting proxy: Between Browser and web application
    b.	Spider
    c.	Passive scanner
    d.	Active scanner
    e.	Fuzzing
    f.	Report generation
    g.	ZAP Extensions available
    h.	Can be extended: Open Source
    i.	Dynamic SSL Certificates
//-------------------------------------------------------------------------------------------------------------------------------
3.	Installing ZAP & Understanding its features
	  Website: https://www.zaproxy.org/download/

    a.	Main Menu Bar
        i.	File Menu: 	Handles current session
        ii.	Edit Menu:	Changing ZAP Mode, Finding anything, etc
        iii.	View Menu:	Handles display options
        iv.	Analyze Men:	Scan policy
        v.	Report Menu:	Report generation
        vi.	Tools Menu:		Tools & general menu
        vii.	Import Menu:		Importing data
        viii.	Online Menu:		Access to online resources
        ix.	Help Menu:		About & help file, Updates, etc

    b.	Toolbar Menu:		Provides easy access to several options.

    c.	Tree View Window: 		Left hand side. Allows to navigate in URLs.

    d.	Workspace Window:	Right hand side. Shows all requests sent

    e.	Information Window:	
        i.	History Tab:		Shows requests in order they were made.
        ii.	Search Tab:		Allows to search all request & responses.
        iii.	Alerts Tab:		Shows all Alerts.
        iv.	Output Tab:		Shows informational messages.
        v.	+ Icon:		To add tabs.

    f.	Footer bar:	Displays summary of Alerts found and status of main automated tools.
//-------------------------------------------------------------------------------------------------------------------------------
4.	Creating Dynamic SSL Certificate & Importing in Browser

    a.	Start ZAP. Chose “No, I do not want to persist this session at this moment in time”.

    b.	Go to: Tools > Options (last) > Dynamic SSL Certificates. Save the generated certificate at any location on your computer.

    c.	Open Firefox > Menu > Settings > Privacy & Security > Certificates > View Certificates… > Import > Select the downloaded Certificate from ZAP > 
    Open > Tick on “Trust this CA to identify website” > OK > OK on Main Window.

    d.	Certificate imported. This step is necessary to navigate inside browser and see necessary messages.

    e.	Close Firefox
//-------------------------------------------------------------------------------------------------------------------------------
5.	Proxy Web Traffic through ZAP

    a.	Start ZAP and check Proxy running status at Footer Bar.

    b.	Go to: Tools > Options > Local Proxies > set Address as localhost & Port as 8081 > OK.

    c.	Check changed Port No at Footer Bar.

    d.	Making changes in Browser
        i.	Open Firefox > Menu > Settings > Network Settings > Select “Manual Proxy Configuration” > HTTP Proxy: 127.0.0.1 > Port No 8081 > Tick 
	“Also use this proxy for HTTPS > OK.

        ii.	Open any website. All messages will start getting logged in History Bar.

        iii.	You may see “site steps” in Tree Window.

        iv.	You may see ZAP HUD Window. Click on “Do not show this screen again” > Click “Continue to your target”.
//-------------------------------------------------------------------------------------------------------------------------------
6.	Configure FoxyProxy
    a.	Open Firefox > Menu > Settings > Network Settings > Select “No proxy”

    b.	Go to: addons.mozilla.com > Search for FoxyProxy Standard > Add to Firefox.

    c.	Open ZAP > Tools > Options > Local Proxies > Check for: Address: localhost & Port No: 8081

    d.	Open Firefox > Click on FoxyProxy > Add > Name it “ZAP” > Proxy Type: HTTP > IP: 127.0.0.1, Port ID: 8081 > Save.

    e.	Open New Tab in Firefox > Enable ZAP from FoxyProxy > Open any website > Traffic will get captured in ZAP.
//-------------------------------------------------------------------------------------------------------------------------------
7.	Installing Mutillidae
//-------------------------------------------------------------------------------------------------------------------------------
8.	Intercepting request with ZAP (Man in the Middle Attack-MITM)
    a.	Open Mutillidae > Login > Start FoxyProxy for ZAP > Username: admin & Password: adminpass.

    b.	It will get captured in ZAP.

    c.	Search for login / admin / adminpass in ZAP Search Tab in Info Window.

    d.	Another method: Insert username and password (DO NOT press login)

    e.	Go to Zap. There is a Green Round Button on Tool Bar “Set Break on all requests and response”, click it. Now, go back to Mutillidae and press
    login. Username and password will get captured automatically and will be reflected in Workspace window.

    f.	Everything being captured under breakpoint:	“Submit and step to next request or response” button & “Submit and continue to next breakpoint” 
    buttons are adjacent to Green Button “Set Break on all request and response”.

    g.	Now, everything done on Mutillidae page will be stopped at every breakpoint in ZAP.

    h.	Changing Captured Username and Password: The username or password captured using “Set Break on all request and response” Green Button can 
    be changed and then be forwarded using “Submit and continue to next breakpoint” forward arrow button.
//-------------------------------------------------------------------------------------------------------------------------------
9.	Intercepting specific request with ZAP
    Case 01:
    a.	Let’s say we want to capture “DNS Request” page from Mutillidae.

    b.	Open Mutillidae > Login (admin & adminpass) > OWASP Top 10 > A1-Injection > Command Injection > DNS Lookup.

    c.	Go to ZAP. In Information Window, select “DNS Request” request. In Workspace window, go to Request Option on top. Confirm whether it is same thing 
    you are looking for.

    d.	Back in Information Window, select “DNS Request” request (So that you can focus particularly on “DNS Request”) > right click >

        i.	Select “Break…”
        ii.	Or, select “Show in Sites Tab” > Now, go in Tree View Window (left) to see where is that site > right click and select “Break…” Option.

    e.	Change Location, Match & String Option accordingly. In string, delete everything before “page” (keep only: “page\=dns-lookup\.php”)

    f.	Now, where ever I go on webpage and whatever I click, it will be getting logged in ZAP but ZAP will not put any Breakpoint. But, if I go back on 
    “DNS Request” page, ZAP will capture the data and put a Breakpoint on webpage.

    g.	Also, “Submit and step to next request or response” button & “Submit and continue to next breakpoint” buttons will get enabled.

    h.	Also, in Information Window, an additional tab called “Breakpoints” must have been created which shows all manually created Breakpoints.

    Case 02:

    i.	To amend already created Breakpoint:	Go to Breakpoint tab in Information window > Double click already created Breakpoint > Location: “Request   
    Body”, Match: “Regex” & String: “dns-lookup-php-submit-button” (this is the new string we want to search which capturing data packet)

    j.	Now, go back to Mutillidae page. Whatever you do will get registered in ZAP but it will not put any Breakpoint. But, if you search any IP Address 
    in DNS Lookup option, the moment you press “DNS Lookup” Button, it will get captured (as it will match “dns-lookup-php-submit-button”).

    Case 03:

    k.	Capturing text entered in text box: Suppose we want to capture IP Address “1.2.*” (i.e. anything starting from 1.2.x.x).

    l.	Go to Breakpoint created inn Information Window Breakpoints Tab. Double Click. Amend String: “1.2.*”

    m.	Again go to Mutillidae and enter IP starting from 1.2.x.x, it will get captured.

//-------------------------------------------------------------------------------------------------------------------------------

10.	Manually explore for Vuln Assessment in ZAP
    a.	Open ZAP and click on “Manual Explore” option in Workspace Window. Select the Browser “Firefox”. Enter the website to be examined.

    b.	      It will open webpage in Browser. No need to set FoxyProxy.

    c.	Even if we open Firefox externally and browse any page, it will not be recorded in ZAP.

    d.	     Go to Alerts in Information Window to check Vulns manually.

//-------------------------------------------------------------------------------------------------------------------------------

11.	Spidering a Website with OWASP
    a.	      Set of URLs being explored by Spider are called Seeds.

    b.	To open Spider, go to Information Window and click + Icon and select Spider > New Scan > Starting Point > Insert website to be Crawled 
    “192.168.0.186/Mutillidae” > Context and User Option to be left blank as of now > Recurse (if selected then all the nodes under the selected Start  
    Point will also be Crawled by Spider) > Spider Subtree Only (only options available under Starting Point will be Crawled) > Start Scan 

    c.	All URLs found, Nodes Added & Messages sent will be mentioned in Information Window.

    d.	In Tree View Window, in site tree, all the webpages found by Spider will have Spider logo in front of it.

    e.	If you Right Click on any found page in Site Tree Chart > Attack > Spider > Again in Starting Point chose “Select…” option > You can select that 
    from which page your Spider should start Crawling > Start Scan

    f.	Additional pages found will get listed.

    g.	Also, in Information Window (adjacent to New Scan), there is a Progress option where you can select and see all previous scan results too.

    h.	Go to Alert Tab to see details of Alerts generated

    i.	Go to Spider Tab, there is a Settings Gear on Right side. Same can be accessed from Tools > Options > Spider

    Spider Options
        i.	Max Depth to Crawl: 0 means unlimited
        ii.	No of Threads used: Increasing thread will make it slow.
        iii.	Max Duration: 0 min means infinite.
        iv.	Query parameter handling: 
            ia.	Ignoring parameters completely: 
                If URL www.testing.com/?foo=123 is visited then
                www.testing.com/?bar=345 will not be visited.

            ib.	Only parameters name:
                If URL www.testing.com/?foo=123 is visited then
                www.testing.com/?foo=345 will not be visited but 
                www.testing.com/?bar=345 will be visited.

            ic.	Considering both parameter’s name & value:
                If URL www.testing.com/?foo=123 is visited then
                www.testing.com/?foo=345 will be visited but 
                www.testing.com/?bar=345 will also be visited.

//-------------------------------------------------------------------------------------------------------------------------------

12.	Automated Vuln Assessment of a Single Page in ZAP
    a.	Open Mutillidae and login using wrong username and password. This will get captured in ZAP as POST request. Click that POST request on Information 
    Window > Right Click > “Show in Site Map”.

    b.	In Tree View Window, corresponding site will get selected > Right Click > Attack > Active Scan > Let default settings like as it is > Start Scan

    c.	A new tab called “Active Scan” will open in Information Window.

    d.	Vuln in that page can be seen in Alerts Tab.

//-------------------------------------------------------------------------------------------------------------------------------

13.	Automated Vuln Assessment of Entire Site in ZAP
    a.	Open ZAP > Automated Scan > Paste URL in “URL to Attack”.

    b.	For Automated Scan either Ajax Spider is used or traditional spider.

    c.	Attack!

    d.	Spider tab will get activated in Information window. It will start enumerating DNS associated.

    e.	Once the Spidering is completed, it will switch to Active Scan.

    f.	As the problems are found, it will be reflected in Alerts.

    g.	Summary of Alerts can be seen in Footer Bar

//-------------------------------------------------------------------------------------------------------------------------------

14.	Automated Vuln Assessment of a Partial Site in ZAP
    a.	Once ZAP and Mutillidae are started, ZAP starts capturing site contents in Tree View Window as folders. 

    b.	Any one folder can be selected and Active Scan can be performed on it. No additional folders will get added in Tree View as the scan is being 
    conducted on one particular folder only.

//-------------------------------------------------------------------------------------------------------------------------------

15.	Generating Vuln Assessment Report in ZAP
    a.	Let’s say you started manual testing on a website. 

    b.	In Tree View Window, select and delete all those websites which are not required in the report.

    c.	Go to Report > Generate Report > Mention location and other options about report generation > Generate Report

    d.	Report will be opened in the Browser. 

    e.	Links mentioned in the report can be generated as a file too. Go to Report > Export All URLs to File…

    f.	To change risk level / severity of any Alert:	Go to Alert > Select the alert highlighted > Right Click > Edit > Change severity > Save

//-------------------------------------------------------------------------------------------------------------------------------

16.	Contexts, scope and Modes in ZAP
    a.	Contexts:	It is a way of relating a set of URLs together. Context generally corresponds to a web application being tested. Contexts are defined as 
    a set of regular expressions using Regex. Contexts can be configured via:
        i.	The Session Contexts dialogs
        ii.	Right click menu items in Site Tab.
        iii.	Right click menu items in History Tab

    b.	Configuring Context: Method 1

        i.	Select the site folder in Tree View Window. File Menu > Session Properties… (Control + Alt + P) > Under Contexts: “1: Default Contexts” : 
	“1: Include in Context” > Add > Type site name including * (eg http://192.168.0.186/mutillidae.*)

        ii.	OK

        iii.	Icons will get changed in Tree View Window of all folders and subfolders related to this Context.

    c.	Configuring Context: Method 2

        i.	Right click on the folder in Tree Window > “Include in Context” > “Default Context” > 

        ii.	The URL will be automatically added with the Regex.

        iii.	OK

        iv.	Icons will get changed in Tree View Window of all folders and subfolders related to this Context.


    d.	Configuring Context: Method 3

        i.	Select URL from History tab in Information window.

        ii.	Right Click > Include in Context > …same process.

    e.	Scope
        i.	Scope is set of URLs you are testing which are part of Context.

        ii.	Scope is defined by Context you have specified.

        iii.	By default nothing is in scope.

    f.	Configuring Scope
        i.	If you go to File > Session Properties > “1: Default Context” > “In Scope” check box is already ticked by Default.

        ii.	Go to Tree View, there is an icon (like aiming mark at top left) which is “Show only URLs in Scope”. Similar icon is on history tab.

    g.	Modes (ZAP Modes)
        i.	     Safe Mode: No potentially dangerous operations are permitted.

        ii.	Protected Mode: You can perform (potentially) dangerous actions on URLs in the Scope only.

        iii.	     Standard Mode: You can do anything.

        iv.	Attack Mode: New nodes that are in Scope are Actively Scanned as they are discovered. 

//-------------------------------------------------------------------------------------------------------------------------------

17.	Sessions in ZAP (first screen pop in start)
    a.	Persisting a session:
        i.	Stored in a local database.

        ii.	No need to save as everything is being saved.

        iii.	Much faster to persist a session at the start.

        iv.	If you close ZAP without persisting your session, then you will not be able to access it again.


    b.	If you did not see the pop up window, go to Tools > Options > Database > Tick “Prompt for Persistence options on new session” 

    c.	Restart ZAP or New Session. You will see the prompt.

    d.	“Yes, I want to persist this session with name based on the current timestamp”: ZAP will store the session in default directory with name as per 
    current timestamp.

    e.	“Yes, I want to persist this session but I want to specify the name and location”: Self understood

    f.	“No, I do not want to persist this session at this moment in time”: Still session can be persisted. Go to File > “Persist Session”.

    g.	Comparing Sessions: Save two sessions. Open first session.

        i.	Go to Report > “Compare with Another Session” > It will ask for another session (click on second session) > It will ask for another file 
	name 
        where both first and second session comparison will be stored.

        ii.	It will open up the Browser with Comparison Results. 

        iii.	You can see results of: First session alone, second session alone, Any Session separately and Common files between both the session.

    h.	To exit & delete session: File > “Exit and Delete Session…”

    i.	Saving current session as Snapshot: File > “Snapshot Session As…”

    j.	Even if the session is deleted, still snapshot will be there to get the data back.

//-------------------------------------------------------------------------------------------------------------------------------

18.	ZAP Request Editor
    a.	In Mutillidae website > Login > “OWASP Top 10” > “A5 – Cross Site Request Forgery (CSRF)” > “Add to your Blog”

    b.	Add a Blog “This is a test Blog” > “Save Blog Entry”

    c.	You can see the entry must have been saved in the Blog Entry Table below.

    d.	Go to ZAP. Look for “This is a test Blog” POST entry in the History tab. Right click on it > “Open/Resend with Request Editor…” (ensure that you 
    are not in safe mode, or else this option will not be enabled)

    e.	Manual Request Editor will open (akin to Repeater of Burp Suite)

        i.	It has Request & Response Tabs
        ii.	You can resend the request after making changes.

        iii.	On left top of Request Tab, there is Method Option, Header: Text Option, Body: Table, Cobine display or header & Body, also, Split display 
        of header & body, Accept Cookies, Follow Redirects, Update Content length, Regenerate Anti-CSRF Token, Separate tabs for Request and Response, 
        etc.

        iv.	Change the message captured i.e. from “This is a test Blog” to “This is another test Blog” > Send it.

        v.	Go back to History Tab in Information Window > You will see another entry with a Hand Icon (i.e. Manual). 

        vi.	If you go back in Mutillidae > Press Back Button > you will see another entry being made with “This is another test Blog”.

        vii.	Back in ZAP, you can change username and uid to make entry by someone else’s name too.

        viii.	Server side validations are implemented to prevent such types of attacks.

//-------------------------------------------------------------------------------------------------------------------------------

19.	Passive Scan Rules in ZAP
    a.	Passive Scan Rules define what kind of vuln to check for in the background:
        i.	Application Errors.
        ii.	Cookie without same site attribute
        iii.	Cookie HTTPOnly
        iv.	Cross Domain Script Inclusion
        v.	Info disclosure in URLs
        vi.	Info disclosures in comments

    b.	To configure Passive Scan Rules: Go to Tools > Options > Passive Scan Rules.

    c.	Here it is defined that how ZAP will define this Vuln (Medium/High/etc).

    d.	Passive Scanner: There is another option in Options window called “Passive Scanner” where some other configurations can be done.

    e.	Passive Scan Tags: Tags are small piece of texts associated with Request.

    f.	Eye Icon in Footer Bar: Shows Passive Scan Queue. Some value will be displayed when Passive Scan is running and will become Zero when Scanning is 
    complete.

//-------------------------------------------------------------------------------------------------------------------------------

20.	Active Scanning in ZAP
    a.	Active scan can find only certain types of Vulns. Logical vuln like Broken Access Control will not be found using Active Scan. 
    b.	Some examples of Active Scan Rules are:
        i.	.htaccess Information Leak
        ii.	Code Injection
        iii.	Command Injection
        iv.	Cross Site Scripting
        v.	Directory Browsing
        vi.	SQL Injection

    c.	How & where to configure Active Scan Rules-1:
        i.	      Look for “Scan Policy Manager…” symbol in toolbar. 
        ii.	You will see Default Policy mentioned > Modify > Not doing much now.
    d.	How & where to configure Active Scan Rules-2:
        i.	Tools > Options > Active Scan > …change accordingly.
        ii.	Tools > Options > Active Scan Input Vectors > …change accordingly.
	
//-------------------------------------------------------------------------------------------------------------------------------

21.	ZAP Scan Policy
    a.	Look for “Scan Policy Manager…” symbol in toolbar > You will see Default Policy mentioned > Modify > …change accordingly.

    b.	To create a New Policy (Suppose to test only XSS): “Scan Policy Manager…” > “Scan Policy” > Put name at Policy: “XSSTest” > Apply OFF Threshold To 
    All Rules GO…(so this will not run any of the tests now)

    c.	Now, go to Injection > Select Cross Site Scripting (Persistent) Option > Medium… (now it will test for XSS Only).

    d.	Click on Login page (anyone) found in History tab > Right click > Active Scan > Policy > you will see XSSTest policy there.

//-------------------------------------------------------------------------------------------------------------------------------

22.	Attack Mode
    a.	It is similar to active scanning mostly.
    b.	Select Attack Mode > Active Scan Tab will get added in Information Window
    c.	Select a target website > It will start Active Scan automatically
    d.	As soon as you go to new page in browser and if it is in scope, it will start attacking.
    e.	You can have a different policy for attack mode:
        i.	This can be used if you want to exploit for any specific vuln in the application.
        ii.	Tools > Options > Active Scan > Attack Mode Scan Policy “select the XSSTest” (created earlier).
        iii.	Now if anything is added to scope, this time the Attack Mode will use XSSTest only.
        iv.	Also, in this specific policy, we can specify High Strength. (Go to Scan Policy Manager > Click on XSSTest > Modify > Injection > Cross 
	Sight 
        Scripting .. > High Strength
	
//-------------------------------------------------------------------------------------------------------------------------------
Follow me at:
(a) Insta: 	@tech.challenged
(b) Twitter:	@_techchallenged
//-------------------------------------------------------------------------------------------------------------------------------

