# projector-client-web
A web client for Projector.

## Building
```shell script
./gradlew :projector-client-web:browserProductionWebpack
```

This will build the client files in the `projector-client-web/build/distributions` dir.

## Running
After building, you can run the HTML page: `projector-client-web/build/distributions/index.html`.

## Notes
Tested browsers:
- Chromium.
- Firefox.

## Page parameters
You can set some settings in query parameters like this: `index.html?host=localhost&port=8887&wss`. Actual list of parameters can be found in the `ParamsProvider.kt` file. Here we describe them.

### Main parameters
Name | Type | Default value | Description 
---|---|---|---
`host` | String | Host of the web page | Set the host of `projector-server` to connect.
`port` | String | `8887` | Set the port of `projector-server` to connect.
`wss` | Presence | Protocol of the web page | Enable security of WebSocket connection.
`token` | String? | Not present | Set a password which will be checked by the server on the connection.
`mobile` | String? | Not present | Enable overlay controls handy for mobile devices. Presented param activates all controls. Provide `onlyButtons` value if you don't use virtual keyboard. 

### Debug/test parameters
Name | Type | Default value | Description 
---|---|---|---
`clipping` | Presence | Not present | Show borders of clipping areas via red and blue lines.
`logUnsupportedEvents` | Presence | Not present | Log unsupported events received from server to browser console.
`doubleBuffering` | Presence | Not present | Enable double buffering for every single message from server.
`enableCompression` | Presence | Not present | Use compression for sending and receiving WebSocket messages.
`toClientFormat` | String | `jsonManual` | Sets format of data from server to client: `json`, `jsonManual`, `protoBuf`.
`imageTtl` | Double | `60_000.0` | Set caching time of unused images in ms.
`flushDelay` | Int? | `1` | Set buffering time of events from client in ms. If the value is not integer, unbuffered mode is used: every client event is sent to the server immediately.
`showTextWidth` | Presence | Not present | Show near-text lines of browser width and desired width.
`showSentReceived` | Presence | Not present | Show blinking indicators in the corner of the screen when events were sent or received.
`showPing` | Presence | Not present | Show some info of simple ping to and from server.
`pingAverageCount` | Int? | Not present | Activate displaying average ping of this number of iterations.
`backgroundColor` | String | `2A2` (green) | Set color of area where there are no windows.
`userScalingRatio` | Double | `1.0` | Set scaling ratio.
`pingInterval` | Int | `1000` | Set interval of pinging in ms.
`showProcessingTime` | Presence | Not present | Log processing time of server messages to browser console.
`repaintArea` | Presence | Not present | Enable ability to see repainted areas, use a shortcut to toggle (more info below).
`speculativeTyping` | Presence | Not present | Enable rendering symbols in Editor not waiting for draw events from server.

## Shortcuts
- `Ctrl + F10` prints statistics to the browser console. Example:  
```
[INFO] :: ClientStats :: Stats:

simple ping average:                    20.84 (19 iterations)
to-client message size average:         3K bytes (185 iterations)
to-client compression ratio average:    1.00 (185 iterations)
draw event count average:               56 (185 iterations)
decompressing time average:             0.00 ms (185 iterations)
decoding time average:                  12.51 ms (185 iterations)
drawing time average:                   3.11 ms (185 iterations)
other processing time average:          0.20 ms (185 iterations)
total (sum) time average:               15.83 ms (185 iterations)

to-client message size rate:    30K bytes per second (21.7 seconds)
draw event count rate:          477 per second (21.7 seconds)
decompressing time rate:        0.04 ms per second (21.7 seconds)
decoding time rate:             106.65 ms per second (21.7 seconds)
drawing time rate:              26.52 ms per second (21.7 seconds)
other processing time rate:     1.72 ms per second (21.7 seconds)
total (sum) time rate:          134.92 ms per second (21.7 seconds)

Stats are reset!
```
- `Ctrl + F11` toggles showing repainted areas (if `repaintArea` query param is enabled).
