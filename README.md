
# Tradingview
<br>
Restful API access for managing tradingview indicator access.

<h1>Installation</h1>
Follow below steps to install and run the API service
<h3>Run locally, on a VPS or on Replit</h3>

<h3>Update environment variables</h3>
Only environment variables to be updated are:
<ul>
<li>username - Your tradingview username</li>
<li>password - Your tradingview password</li>
</ul>
(A Premium Tradingview subscription is required.)

<h1>Usage</h1>
Once up and running, you will be able to use following calls to manage Tradingview access.

<h3>GET /validate/{username}</h3>
Can be used to validate username. This can be handy operation to execute before trying to execute access management for the user. If user is not valid, we can stop the workflow then and there.
<p>
<ul>
<li><b>Payload</b> - None</li>
<li><b>Headers</b> - None</li>
<li><b>Returns</b> - JSON output with following information:</li>
<ol>
<li><b>validUser</b> - Can be true or false. Tells whether username passed is valid or not.</li>
<li><b>verifiedUserName</b> - returns the exact username as in Tradingview records (along with matching case). If validUser is false, this field will also have blank value.</li>
</ol>
</ul>
<pre>
{
    "validuser": true,
    "verifiedUserName": "ApolloAlgo"
}
</pre>


<h3>GET /access/{username}</h3>
This method can be used to get the current access level of user for particular publications identified by pine_ids
<p>
<ul>
<li><b>Payload</b> - Json Payload containing list of pine ids</li>
<ol>
<li><b>pine_ids</b> - Array of pine ids. Pine ids are backend unique ids for each script. We can get these ids from browser developer console when script is loaded or when access methods are performed on the tradingview UI. Please note, only Pine Ids for scripts which belong to your account will work in this way. You will not be able to control the access to scripts which are not yours.</li>
<pre>
{
    "pine_ids" : ["PUB;0fc414298ba34d61866a7817b6eec7b4", "PUB;b48044bbad454132bbcd3aa51807da96"]
}
</pre>
</ol>
<li><b>Headers</b> - None</li>
<li><b>Returns</b> - JSON output array with following information:</li>
<ol>
<li><b>pine_id</b> - Pine publication id which is sent as input to the API request</li>
<li><b>username</b> - Username against which the operation is performed.</li>
<li><b>hasAccess</b> - true if user already has access to script. false otherwise</li>
<li><b>noExpiration</b> - true if user has non expiring access to script. false otherwise</li>
<li><b>currentExpiration</b> - applicable only if hasAccess is true and noExpiration is false. Ignore otherwise.</li>
</ol>
</ul>
<pre>
[
    {
        "pine_id": "PUB;0fc414298ba34d61866a7817b6eec7b4",
        "username": apolloalgo",
        "hasAccess": false,
        "noExpiration": false,
        "currentExpiration": "2023-07-17 06:27:49.067935+00:00"
    },
    {
        "pine_id": "PUB;b48044bbad454132bbcd3aa51807da96",
        "username": "apolloalgo",
        "hasAccess": false,
        "noExpiration": false,
        "currentExpiration": "2023-07-17 06:27:49.196514+00:00"
    }
]
</pre>

<h3>DELETE /access/{username}</h3>
This method can be used to remove the current access level of user for particular publications identified by pine_ids
<p>
<ul>
<li><b>Payload</b> - Json Payload containing list of pine ids</li>
<ol>
<li><b>pine_ids</b> - Array of pine ids. Pine ids are backend unique ids for each script. We can get these ids from browser developer console when script is loaded or when access methods are performed on the tradingview UI. Please note, only Pine Ids for scripts which belong to your account will work in this way. You will not be able to control the access to scripts which are not yours.</li>
<pre>
{
    "pine_ids" : ["PUB;0fc414298ba34d61866a7817b6eec7b4", "PUB;b48044bbad454132bbcd3aa51807da96"]
}
</pre>
</ol>
<li><b>Headers</b> - None</li>
<li><b>Returns</b> - JSON output array with following information:</li>
<ol>
<li><b>pine_id</b> - Pine publication id which is sent as input to the API request</li>
<li><b>username</b> - Username against which the operation is performed.</li>
<li><b>hasAccess</b> - true if user had access to script before removing access. false otherwise</li>
<li><b>noExpiration</b> - true if user had non expiring access to script before removing access. false otherwise</li>
<li><b>status</b> - Status of the remove operation</li>
</ol>
</ul>
<pre>
[
    {
        "pine_id": "PUB;0fc414298ba34d61866a7817b6eec7b4",
        "username": "apolloalgo",
        "hasAccess": true,
        "noExpiration": true,
        "currentExpiration": "2023-07-17 06:28:49.655286+00:00",
        "status": "Success"
    },
    {
        "pine_id": "PUB;b48044bbad454132bbcd3aa51807da96",
        "username": "apolloalgo",
        "hasAccess": true,
        "noExpiration": true,
        "currentExpiration": "2023-07-17 06:28:49.923866+00:00",
        "status": "Success"
    }
]
</pre>

<h3>POST /access/{username}</h3>
This method can be used to add/update current access level of user for particular publications identified by pine_ids. 
<p>
<ul>
<li><b>Payload</b> - Json Payload containing list of pine ids</li>
<ol>
<li><b>pine_ids</b> - Array of pine ids. Pine ids are backend unique ids for each script. We can get these ids from browser developer console when script is loaded or when access methods are performed on the tradingview UI. Please note, only Pine Ids for scripts which belong to your account will work in this way. You will not be able to control the access to scripts which are not yours.</li>
<pre>
{
    "pine_ids" : ["PUB;0fc414298ba34d61866a7817b6eec7b4", "PUB;b48044bbad454132bbcd3aa51807da96"]
}
</pre>
</ol>
<li><b>Headers</b> - None</li>
<li><b>Returns</b> - JSON output array with following information:</li>
<ol>
<li><b>pine_id</b> - Pine publication id which is sent as input to the API request</li>
<li><b>username</b> - Username against which the operation is performed.</li>
<li><b>hasAccess</b> - true if user already has access to script. false otherwise</li>
<li><b>noExpiration</b> - true if user has non expiring access to script. false otherwise</li>
<li><b>currentExpiration</b> - applicable only if hasAccess is true and noExpiration is false. Ignore otherwise.</li>
<li><b>expiration</b> - New expiration applied after applying access update.</li>
<li><b>status</b> - Status can be Success, Failure, or Not Applied. Not Applied will be returned if user already has lifetime access to given script and no further addition is possible.</li>
</ol>
</ul>
<pre>
[
    {
        "pine_id": "PUB;0fc414298ba34d61866a7817b6eec7b4",
        "username": "apolloalgo",
        "hasAccess": true,
        "noExpiration": true,
        "currentExpiration": "2022-09-17T06:28:25.933303+00:00",
        "expiration": "2022-09-17T06:28:25.933303+00:00",
        "status": "Success"
    },
    {
        "pine_id": "PUB;b48044bbad454132bbcd3aa51807da96",
        "username": "apolloalgo",
        "hasAccess": true,
        "noExpiration": true,
        "currentExpiration": "2022-09-17T06:28:26.191805+00:00",
        "expiration": "2022-09-17T06:28:26.191805+00:00",
        "status": "Success"
    }
]
</pre>

## Contributions & Thanks
If you found this project interesting or useful, create accounts with my referral links:
- [Tradingview](https://www.tradingview.com/gopro/?share_your_love=d3f4ult)
- [WeBull](https://a.webull.com/8XVR7o9KJloSNSMbsX)
- [BingX](https://bingx.com/en-us/partner/D3f4ult)
- [FundedEngineer](https://dashboard.fundedengineer.com/evaluation?affiliateid=d3f4ult)
- [UnusualWhales](http://unusualwhales.com/referral#d3f4ult)
- [TraderSync](https://www.tradersync.com/?ref=d3f4ulttrades)

# Profiles
<a href="https://twitter.com/ApolloAlgo"><img src="https://i.pinimg.com/originals/aa/3d/75/aa3d750ddec109594ac7c89cb8cbabab.jpg" width="100" height="100"></a>
<a href="https://discord.gg/ApolloAlgo"><img src="https://i.pinimg.com/originals/b6/fe/4a/b6fe4a830e0263d8344b63e3dbcf3033.jpg" width="100" height="100"></a>
<a href="https://youtube.com/ApolloAlgo"><img src="https://i.pinimg.com/originals/f4/14/b8/f414b816ef11df2c1eaae61f2fc8c489.jpg" width="100" height="100"></a>
