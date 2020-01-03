# ServerEvents
Creates a 24hr event cycle with daily player logins, login streaks, and events to provide data

ServerEvents aims to provide a platform that other plugins can use to register events in a 24hr event cycle.
It takes care of some of the basics and provides tools to allow plugin developers to add their own features.
Records daily logins and login streaks
Records last login time
Provides a REST API endpoint for accessing the above data
Allows for setting the hour and minute at which the plugin will raise its reset event (i.e., the daily server reset)
Allows for registering methods to be run every x hours/minutes/seconds
Allows for retrieving Login Data for any recorded user. Login Data can include: 
daily login status (true or false)
last login time
login streak (increased by successive daily logins)
Allows for adding new SqlTables into the ServerEvents database
Allows for reading and writing to the ServerEvents database
Provides an OnPlayerLogin event which passes on Login Data
Provides an OnServerReset event which is triggered once per day at the set reset hour+minute
REST
ServerEvents provides a REST API endpoint: /serverevents/logindata?id={value}. No token is required. {value} must be a valid user ID. Output follows the following example:
Code:
{
  "status": "200",
  "response": {
    "UserID": 1,
    "LastLoginDateString": "2016-01-22 07:42:58",
    "LoginStreak": 3,
    "HasLoggedIn": true
  }
}
Plugins
ServerEvents is designed to be used by other plugins. The Source URL (alt) provides a link to an example plugin, but you can also access it here.

Basics:
Code:
ServerEventsPlugin EventsPlugin;
public override void Initialize()
{
    EventsPlugin = (ServerEventsPlugin)ServerApi.Plugins.Select(p => p.Plugin).First(plugin => plugin.Name == "Server Events");
    EventsPlugin.OnPlayerLogin += EventsPlugin_OnPlayerLogin;
}

public void EventsPlugin_OnPlayerLogin(TSPlayer player, LoginData loginData)
{
    Console.WriteLine($"PLAYER {player.Name} HAS LOGIN STREAK: {loginData.LoginStreak}");
}

[ServerEvents](https://tshock.co/xf/index.php?resources/server-events.147/)
