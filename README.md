# Inflatable Last.fm .NET SDK

![Project logo](./res/if-lastfm-logo-300.png)

[![Code licence](https://img.shields.io/badge/licence-MIT-blue.svg?style=flat)](LICENCE.md)

## Maintenence help wanted

Hi there! The maintainer of this library @rikkit is now mostly a TypeScript + React dev, and has been for the last several years. Since this is a .Net library, the maintainer will probably not be able to keep it up-to-date to the latest .Net standards. If you spot something wrong, please file and issue or better yet, a pull request. Thanks!

## Project Goals

- To provide complete .NET bindings for the Last.fm REST API
- To build useful components for Last.fm applications
- To be the very best, like no-one ever was

## Description

The Inflatable Last.fm .NET SDK is a comprehensive library that provides .NET bindings for the Last.fm REST API. This SDK aims to simplify the process of integrating Last.fm functionality into .NET applications, allowing developers to easily access and manipulate Last.fm data.

## Features

Key features of this SDK include:

- **Complete API Coverage**: Provides bindings for all Last.fm API methods, allowing full access to Last.fm's extensive music data and user information.
- **Asynchronous Operations**: Utilizes `async/await` patterns for efficient and non-blocking API calls.
- **Strong Typing**: Offers strongly-typed objects for Last.fm entities like artists, albums, and tracks, enhancing code reliability and developer productivity.
- **Authentication Support**: Implements Last.fm's authentication protocols, enabling both authenticated and non-authenticated API requests.
- **Scrobbling Capabilities**: Includes methods for scrobbling tracks to Last.fm, a core feature of the Last.fm service.
- **Extensible Architecture**: Designed with extensibility in mind, allowing for easy updates as the Last.fm API evolves.
- **Cross-Platform Compatibility**: Targets `.NET Standard 1.1`, ensuring broad compatibility across various .NET platforms.

## Contributing

Input is always welcome! [Raise an issue on GitHub](https://github.com/inflatablefriends/lastfm/issues), or send a message to [the Gitter chatroom](https://gitter.im/inflatablefriends/lastfm) if you need help with the library.

If you're interested in contributing code or documentation, [this short introduction to the library](doc/contributing.md) will help you get started.

## Quickstart

### Installing

#### NuGet Package Manager

1. Open your project in Visual Studio.
2. Right-click on your project in the Solution Explorer and select "Manage NuGet Packages".
3. In the "Browse" tab, search for "Inflatable.Lastfm".
4. Click on the package and select "Install".

Alternatively, you can use the Package Manager Console:

Install [Inflatable.Lastfm](https://www.nuget.org/packages/Inflatable.Lastfm/) from NuGet.

#### .NET CLI

For projects using the .NET CLI, use the following command:
`dotnet add package Inflatable.Lastfm`

#### NuGet - prerelease code

1. Install the [.NET Core SDK](https://docs.microsoft.com/en-us/dotnet/core/install/sdk)
2. Clone this repo and checkout to the commit you need
3. Run `dotnet pack`
4. Reference the built NuGet package file in your project

### Examples

First, [sign up for Last.fm API](http://last.fm/api) access if you haven't already.

Create a LastfmClient:

```c#
var client = new LastfmClient("apikey", "apisecret");
```

Get information about an album:

```c#
var response = await client.Album.GetInfoAsync("Grimes", "Visions");

LastAlbum visions = response.Content;
```

For methods that return several items, you can iterate over the response:

```c#
var pageResponse = await client.Artist.GetTopTracksAsync("Ben Frost", page: 5, itemsPerPage: 100);

var trackNames = pageResponse.Select(track => track.Name);
```

Several API methods require user authentication. Once you have your user's Last.fm username and password, you can authenticate your instance of LastfmClient:

```c#
var response = await client.Auth.GetSessionTokenAsync("username", "pass");

// or load an existing session
UserSession cachedSession;
var succesful = client.Auth.LoadSession(cachedSession);
```

Authenticated methods then work like any other

```c#
if (client.Auth.HasAuthenticated) {
	var response = await client.Track.LoveAsync("Ibi Dreams of Pavement (A Better Day)", "Broken Social Scene");
}
```

### Troubleshooting

#### Common Issues:

1. **Authentication Failure:** Ensure that your API key and secret are correctly passed to `LastfmClient`. Also, verify your credentials with Last.fm.
2. **Timeout Errors:** Increase the timeout in your HTTP client settings if you encounter long API response times.
3. **Compatibility Problems:** Check the .NET Standard version compatibility with your project. Review the platform compatibility section for further guidance.
4. **Rate Limiting Issues:** If you encounter frequent `429` errors, you may be exceeding Last.fm's rate limits. Implement appropriate delays between requests.

For more detailed troubleshooting, please refer to the [Last.fm API documentation](https://www.last.fm/api) or open an issue on our [GitHub repository](https://github.com/inflatablefriends/lastfm/issues).

## Documentation

- [API method progress report](PROGRESS.md)
- [Contributing](doc/contributing.md)
- [Scrobbling](doc/scrobbling.md)
- [Dependency Injection](doc/dependency-injection.md)
- [Example Windows Phone app](https://github.com/inflatablefriends/lastfm-samples)

## Platform Compatibility

The main package targets `netstandard1.1`. Development is on the `master` branch.

### Dependencies

- Newtonsoft.Json 9.0.1 =<
- System.Net.Http 4.3.0 =<

### Supported platforms

Check [this table](https://docs.microsoft.com/en-us/dotnet/articles/standard/library#net-platforms-support) for supported platforms.

### Other platforms

If you need support for a .NET platform that doesn't support .Net Standard 1.1, first see if the feature you need is available in v0.3 or earlier - that version targeted PCL profile 259, and so is compatible with e.g. Windows 8.0 and Windows Phone 7.

If you need a feature for these older platforms, please raise an issue.

## Credits

Maintained by [@rikkilt](http://twitter.com/rikkilt).
Thanks to [all contributors](https://github.com/inflatablefriends/lastfm/graphs/contributors)!
