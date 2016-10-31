# Airstream

Airstream is an iOS / macOS framework for streaming audio between Apple devices using AirPlay.

[ An example gif ]

You can use Airstream to start an AirPlay server in your iOS or macOS applications. Then, any Apple device can stream audio to your application via AirPlay, with no extra software required.

## Installation

Airstream can be installed by using either CocoaPods, Carthage, or just simply cloning this repository and its submodules in your project.

### CocoaPods

[CocoaPods](https://cocoapods.org/) is a dependency manager for Swift and Objective-C Cocoa projects. You can install it with the following command:

```bash
$ gem install cocoapods
```

Then, to include Airstream in your project, specify it in your `Podfile`:

```ruby
target 'MyApp' do
  pod 'Airstream', '~> 0.1'
end
```

Now you can install Airstream into your Xcode project:

```bash
$ pod install
```

For more information, have a look at [Using CocoaPods](https://guides.cocoapods.org/using/using-cocoapods.html).

### Carthage

[Carthage](https://github.com/Carthage/Carthage) is a decentralized dependency manager for Cocoa.

You can install it using [Homebrew](http://brew.sh/) with the following commands:

```bash
$ brew update
$ brew install carthage
```

Then, to include Airstream in your project, specify it in your `Cartfile`:

```ruby
github "qasim/Airstream" ~> 0.1
```

Now you can install Airstream:

```bash
$ carthage
```

Drag the built `Airstream.framework` into your Xcode project.

## Basic usage

First, initialize and start Airstream somewhere (make sure that it's retained). You'll also want to set its delegate.

```swift
let airstream = Airstream(name: "My Airstream")

airstream.delegate = self
airstream.startServer()
```

That's it! Your own AirPlay server is now up and running. You can gracefully shut it down as well:

```swift
airstream.stopServer()
```

Implement any of the delegate methods to actually make use of Airstream's features, like retrieving a song's album artwork:

```swift
func airstream(airstream: Airstream, didSetCoverart coverart: NSData) {
  // Coverart for the item that's currently streaming
  let image = NSImage(data: coverart)
}
```

## API reference

### Airstream

```swift
func init()
func init(name: String?)
func init(name: String?, password: String?)
func init(name: String?, password: String?, port: Int?)
```

Basic initializers for the Airstream.

-

```swift
func startServer()
```

Starts the AirPlay server and begins broadcasting.

-

```swift
func stopServer()
```

Gracefully shuts down the AirPlay server.

-

```swift
var name: String
```

The AirPlay server's receiver name. This is what is shown to Apple devices when they go to connect to your Airstream. `"My Airstream"` by default.

-

```swift
var password: String?
```

The AirPlay server's receiver password. You can set this to prompt any Apple devices that wish to connect to your Airstream with a password challenge.

-

```swift
var port: Int
```

The port where the AirPlay server should broadcast to. `5000` by default.

-

```swift
var running: Bool
```

Determines whether the server is currently running or not.

-

```swift
var remote: AirstreamRemote?
```

The reference to this Airstream's remote control object, which can be used to send commands to the connected Apple device.

-

```swift
var volume: Float?
```

The connected Apple device's volume.

-

```swift
var metadata: [String: String]?
```

The metadata for the current item being streamed.

-

```swift
var coverart: NSData?
```

The coverart (in binary) for the current item being streamed.

-

```swift
var position: Int?
```

The current position for the current item being streamed.

-

```swift
var duration: Int?
```

The total duration for the current item being streamed.

### AirstreamRemote

### AirstreamDelegate

## Shairplay

Airstream works by depending on a C library called [shairplay](https://github.com/juhovh/shairplay), which is a free portable AirPlay server implementation. You can also visit [qasim/shairplay](https://github.com/qasim/shairplay) for the fork of shairplay that is used by Airstream, which compiles on both iOS and macOS.

## License

Airstream is released under the MIT license. See [LICENSE](./LICENSE) for details.
