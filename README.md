
<!-- TOC -->

- [Introduction](#Introduction)
	- [Bugs](#Bugs)
	- [OAuth2 Clients](#OAuth2-Clients)
	- [Still need some help?](#Still-need-some-help?)
- [OAuth](#OAuth)
    - [Retrieving your client id & secret](#Retrieving-your-client-id-&-secret)
    - [Available scopes](#Available-scopes)
    - [Authorization](#Authorization)
    - [Endpoints](#Endpoints)
	    - [Retrieve user details](#Retrieve-user-details)
	    - [Retrieve user image](#Retrieve-user-image)
	    - [Retrieve user address](#Retrieve-user-address)
	    - [Retrieve user student card](#Retrieve-user-student-card)
	    - [Retrieve user qr code](#Retrieve-user-qr-code)

<!-- /TOC -->

# Introduction

Welcome to the Geevoo Developer Documentation. This documentation is solely dedicated to showcasing the various ways you can utilize Geevoo to create amazing things. Whether you're interessted in enhancing your applications with our API or integrating Geevoo into your software, Geevoo has everything you need to get started.

All our documentation is hosted on GitHub, and we welcome any corrections and improvements from our community. We love collaborating with developers and are always looking for ways to make the development process smoother and more efficient.

## Bugs

If you think you have encountered a bug with our API or wish to report any incorrect information in our documentation, please feel free to create an issue on our [issue tracker](https://github.com/geevoode/docs/issues). In addition to opening an issue on our issue tracker, you can also reach out to us via email at it@geevoo.de if you have any concerns or questions regarding our API or documentation. We're always happy to assist you and appreciate any feedback that helps us improve our services.

## OAuth2 Clients

If you're interested in creating an OAuth2 client with us, we kindly request that you send us an email with the following information:
-   Initiate URL
-   Redirect URL
-   Application Name
-   Purpose of the application / project description
-   List of needed scopes (this won't restrict or affect anything, but we'd like to understand your plans)

You can reach us via email at [it@geevoo.de](mailto:it@geevoo.de) to submit your application details. Our team will review your request and get back to you as soon as possible.

For more information about OAuth2 and how it works, please visit our OAuth2 page. We appreciate your interest in partnering with us and look forward to working together to create amazing applications.

## Still need some help?

In case you have anything on your mind, not being covered on this documentation, feel free to reach out to us anytime.

# OAuth

Geevoo's OAuth2 functionality provides developers with the ability to create powerful applications that leverage authentication and data from the Geevoo API. With our flexible authentication options, developers can create applications that integrate seamlessly with Geevoo and deliver a world-class experience to their users.

## Retrieving your client id & secret

To retrieve the client ID and client secret for your application, you will need to contact us via email with the following information:

1.  Purpose: Explain the purpose of your application and how it will use the Geevoo API.
2.  Initiate URL: Provide the URL where your application will initiate the OAuth2 flow.
3.  Redirect URL: Provide the URL where Geevoo should redirect users after they authorize your application.
4.  Scopes: List the scopes your application requires. Scopes are permissions that control what data the application can access. You can find a list of available scopes under the section [Available scopes](#Available-scopes).

Once we receive this information, we will review your request and provide you with the client ID and client secret. Please note that we may require additional information or clarification before providing access to the Geevoo API.

It is important to keep your client ID and client secret secure. Do not share them with anyone, and take appropriate measures to protect them, such as using secure storage and encryption.

If you have any questions or concerns about using OAuth2 with Geevoo, please do not hesitate to contact us for assistance.

## OAuth2 Endpoints

| Endpoint             | Method | Description                                                                                                                                          |
|----------------------|--------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| /oauth/authorize     | GET    | Displays a page to the user where they can authorize an application to access their protected resources as part of the OAuth2 authorization process. |
| /oauth/token         | POST   | Exchanges an authorization code for an access token as part of the OAuth2 authorization code grant type flow.                                        |
| /oauth/token/refresh | POST   | Requests a new access token using a refresh token as part of the OAuth2 refresh token grant type flow.                                               |

More information and code examples can be found on the official [Laravel documentation](https://laravel.com/docs/8.x/passport#clients-json-api).

## Available scopes
| Scope        | Description                                                                                   |
|--------------|-----------------------------------------------------------------------------------------------|
| user-info    | (Default scope) Get personal information of user such as id, name, email & date of birth.     |
| user-avatar  | Get user avatar if present. Only available using the method ``$user->getAvatar()``.           |
| user-address | Get user address if present. Only available using the method ``$user->getAddress()``.         |
| card         | Get user student card. Only available using the method ``$user->getCard()``.                  |
| qr           | Generate a student qr code. Only available using the method ``$user->getQr(bool $extended)``. |

## Authorization

The general OAuth2 authorization process involves three parties: the resource owner (user), the client application, and the authorization server.

1.  The client application requests authorization from the user to access their protected resources.
2.  The authorization server authenticates the user and requests their permission to grant access to the client application.
3.  If the user grants permission, the authorization server issues an authorization code to the client application.
4.  The client application exchanges the authorization code for an access token by sending a request to the authorization server.
5.  The authorization server validates the authorization code and issues an access token to the client application.
6.  The client application uses the access token to access the user's protected resources.
7.  If the access token expires, the client application can request a new access token using a refresh token.

OAuth2 supports several grant types, including the authorization code grant type, the implicit grant type, the resource owner password credentials grant type, and the client credentials grant type. Each grant type has its own set of requirements and security implications, and the appropriate grant type should be selected based on the specific use case.

## Endpoints

Geevoo provides various endpoints that can be accessed once a user has successfully authenticated through OAuth2. These endpoints allow users to access and interact with their data on Geevoo. Our list of available endpoints is currently growing, and we are continuously adding new ones based on user demand. If you require additional endpoints or functionality, please feel free to request them by submitting an issue on our GitHub issue tracker at [https://github.com/geevoode/docs/issues](https://github.com/geevoode/docs/issues). We are always happy to hear from our users and are committed to improving our platform to better meet their needs.

### Retrieve user details

The `/oauth/user` endpoint requires the `user-info` scope to access and returns basic information about the authenticated user. The response is a JSON object with the following fields:

-   `id`: a unique identifier for the user in UUID format.
-   `first_name`: the user's first name.
-   `last_name`: the user's last name.
-   `email`: the user's email address.
-   `date_of_birth`: the user's date of birth in the format `Y-m-d`.

This endpoint provides a convenient way for client applications to obtain basic information about the authenticated user, such as their name, email, and date of birth. It can be useful for personalizing the user experience or for verifying the user's identity in a secure and reliable way.

### Retrieve user image

The `/oauth/avatar` endpoint requires the `user-avatar` scope to access and returns the user's avatar image as a picture. The response will be the image itself, with the Content-Type set to the mime-type of the image (typically `image/png`).

### Retrieve user address

The `/oauth/address` endpoint requires the `user-address` scope to access and returns the user's address information. The response is a JSON object with the following fields:

-   `street`: the user's street address.
-   `city`: the user's city.
-   `postal`: the user's postal code.

It is important to note that all addresses returned by this endpoint are currently meant to be in Germany. This endpoint can be useful for client applications that need to know the user's address, such as for shipping or billing purposes.

### Retrieve user student card

The `/oauth/card` endpoint requires the `card` scope to access and returns the user's student card as an SVG image. The response will be the image itself, with the Content-Type set to `image/svg+xml`.

### Retrieve user qr code

The `/oauth/qr` endpoint requires the qr `scope` to access and returns a one-time use QR code as an SVG image. The response will be the image itself, with the Content-Type set to `image/svg+xml`.

This endpoint can be useful for client applications that need to provide a QR code for user authentication or verification purposes. It is important to note that the QR code is one-time use only and must be redeemed as soon as it is generated, as it can be invalidated through Geevoo's scanning solution.

The endpoint accepts the query parameter `detailed` as a boolean (either 0, 1, 'true', 'false', '0', '1'). This flag toggles either if detailed informations should be shown when scanning as for example address data.
