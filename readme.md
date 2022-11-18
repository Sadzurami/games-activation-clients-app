# Endless Space Activation Client

A simple application for mass activating game ENDLESS™ Space - Definitive Edition for steams accounts.

# How it works

This application logs into your account, collects some information required for activation, and sends a job to the backend. The server completes your task and activates the game on your account. Simple and quick.

## What kind of info is sent to a third-party service

1. [Steamid](https://help.steampowered.com/en/faqs/view/2816-BE67-5B69-0FEC)
2. [Openid nonce](https://openid.net/specs/openid-connect-core-1_0.html#CodeFlowSteps:~:text=following%20request%20parameters%3A-,nonce,-OPTIONAL.%20String%20value)
3. [Openid sig](https://openid.net/specs/openid-authentication-2_0.html#:~:text=return_to%2Cassoc_handle%2Cresponse_nonce%22.-,openid.sig,-Value%3A%20Base%2064)

## Ditailed pipeline

1. Steam login
2. Cheking game in library
3. Openid auth
4. Creating a task on server side with a returned openid response
5. Waiting task result

# Features

## Import accounts from [farms](https://github.com/JustArchiNET/ArchiSteamFarm)

You can select more than one farm. The search for accounts is recursive.

## Import accounts from file

CSV format: `username:password`

Examples:

-   `user1:pass1`
-   `user2:pass2:email:emailpass`
-   `user3:pass3:otheroptions`

## 2FA auth

Mobile and email guard supported.

## Checking the game's existence

If the game already has an account, the application will go to work with the next account, the current account will be added to the ignore list.

## Requests proxification

Supported protocols: http, https, socks5.

## Import proxies from farm

From the ASF.json file that corresponds to the current account.

## Import proxies from file

Proxies from a file have a higher priority than proxies from the farm, so if both options are provided, the proxy from the file will be selected.

The ip change link is supported, a GET request will be sent. If there is no response from the server or if the server returns a status other than 200, the current execution of the script will fail with an IP address change error.

Examples:

-   `http://user1:pass1@1.2.3.5:1235`
-   `socks://1.2.3.5:1235`
-   `1.2.3.5:1235`
-   `socks://1.2.3.5:1235:https://changeip.com`
-   `https://user1:pass1@1.2.3.5:1235:changeip.com`

## Multithreading

For example, instead of one account, 10 do the same job at the same time. This is much faster, but it is recommended to use only if you have imported the proxy from a file.

## Limiting the number of runs

You can limit the number of script runs by the number of successes or failures.

# Screens

![tab.accounts](./src-docs/tab.accounts.png)
![tab.proxies](./src-docs/tab.proxies.png)
![tab.other](./src-docs/tab.other.png)

# Requirements

-   Windows x64 (7+)
-   1 CPU, 512 MB RAM
-   Internet speed 5MB/s +
