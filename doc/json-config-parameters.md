# JSON Configuration File Options


## General options
  
Attribute      | Default          |Description
---------------|------------------|----------------------------------
`type`         | `equirectangular`| This specifies the panorama type. Can be `equirectangular`, `cubemap`, or `multires`.
`title`        |                  | If set, the value is displayed as the panorama's title. If no title is desired, don't set this parameter.
`author`       |                  | If set, the value is displayed as the panorama's author. If no author is desired, don't set this parameter.
`basePath`     |                  | This specifies a base path to load the images from.
`autoLoad`     |`false`           | When set to `true`, the panorama will automatically load. When `false`, the user needs to click on the load button to load the panorama.
`autoRotate`   |                  | Setting this parameter causes the panorama to automatically rotate when loaded. The value specifies the rotation speed in degrees per second. Positive is counter-clockwise, and negative is clockwise.
`autoRotateInactivityDelay`|      | Sets the delay, in milliseconds, to start automatically rotating the panorama after user activity ceases. This parameter only has an effect if the `autoRotate` parameter is set.
`autoRotateStopDelay`|            | Sets the delay, in milliseconds, to stop automatically rotating the panorama after it is loaded. This parameter only has an effect if the `autoRotate` parameter is set.
`fallback`     |                  | If set, the value is used as a URL for a fallback viewer in case Pannellum is not supported by the user's device. The user will be given the option to click a link and visit this URL if Pannellum fails to work.
`header`       |                  | If this parameter is set, the contents of its value will be inserted into the header of `pannellum.htm`. This is useful if one wants to modify Pannellum's CSS.
`showZoomCtrl` |`true`            | If set to `false`, the zoom controls will not be displayed.
`keyboardZoom` |`true`            | If set to `false`, zooming with keyboard will be disabled.
`showFullscreenCtrl` |`true`      | If set to `false`, the fullscreen control will not be displayed. The fullscreen button will only be displayed if the browser supports the fullscreen API.
`yaw`          | `0`              | Sets the panorama's starting yaw position in degrees.
`pitch`        | `0`              | Sets the panorama's starting pitch position in degrees.
`hfov`         | `100`            | Sets the panorama's starting horizontal field of view in degrees.
`minYaw`, `maxYaw`|`-360` / `360` | Sets the minimum / maximum yaw the viewer can be centered at, in degrees. Defaults to `-360` / `360`, i.e. no limit.
`minPitch`     |`-85`             | Sets the minimum pitch the viewer can be centered at, in degrees. 
`maxPitch`     |`-85`             | Sets the maximum pitch the viewer can be centered at, in degrees.   
`minHfov`      |`50`              | Sets the minimum horizontal field of view, in degrees, that the viewer can be set to.
`maxHfov`      |`120`             | Sets the maximum horizontal field of view, in degrees, that the viewer can be set to.
`compass`      |`false`           | If `true`, a compass is displayed.
`northOffset`  |                  | Set the offset, in degrees, of the center of the panorama from North. As this affects the compass, it only has an effect if `compass` is set to `true`.
`hotSpots`     |                  | This specifies an array of hot spots that can be links to other scenes, information, or external links. Each array element has the following properties.
`hotSpotDebug` |`false`           | When `true`, the mouse pointer's pitch and yaw are logged to the console when the mouse button is clicked.
`sceneFadeDuration`|              | Specifies the fade duration, in milliseconds, when transitioning between scenes. Not defined by default. Only applicable for tours. Only works with WebGL renderer.

### HotSpot specific options

Attribute     | Description
--------------|-----------------------------------------------------
`pitch`       | Specifies the pitch portion of the hot spot's location.
`yaw`         | Specifies the yaw portion of the hot spot's location.
`type`        | Specifies the type of the hot spot. Can be `scene` for scene links or `info` for information hot spots. A tour configuration file is required for `scene` hot spots.
`text`        | This specifies the text that is displayed when the user hovers over the hot spot.
`URL`         | If specified for an `info` hot spot, the hot spot links to the specified URL. Not applicable for `scene` hot spots.
`sceneId`     | Specifies the ID of the scene to link to for `scene` hot spots. Not applicable for `info` hot spots.
`targetPitch` | Specifies the pitch of the target scene.
`targetYaw`   | Specifies the yaw of the target scene.


### `equirectangular` specific options

Attribute        | Default |Description
-----------------|---------|----------------------------------
`panorama`       |         | Sets the URL to the equirectangular panorama image. This is relative to `basePath` if it is set, else it is relative to the location of `pannellum.htm`. An absolute URL can also be used.
`haov`           |`360`    | Sets the panorama's horizontal angle of view, in degrees. This is used if the equirectangular image does not cover a full 360 degrees in the horizontal.
`vaov`           |`180`    | Sets the panorama's vertical angle of view, in degrees. This is used if the equirectangular image does not cover a full 180 degrees in the vertical.
`vOffset`        |`0`      | Sets the vertical offset of the center of the equirectangular image from the horizon, in degrees. This is used if `vaov` is less than `180` and the equirectangular image is not cropped symmetrically.
`ignoreGPanoXMP` |`false`  | If set to `true`, any embedded Photo Sphere XMP data will be ignored; else, said data will override any existing settings.


### `cubemap` specific options

Attribute        | Description
-----------------|----------------------------------------------------
`cubeMap`        | This is an array of URLs for the six cube faces in the order front, right, back, left, up, down. These are relative to `basePath` if it is set, else they are relative to the location of `pannellum.htm`. Absolute URLs can also be used.


### `multires` specific options

Attribute        | Description
-----------------|----------------------------------------------------
`multiRes`       | This contains information about the multiresolution panorama in sub-keys.
`basePath`       | This is the base path of the URLs for the multiresolution tiles. It is relative to the regular `basePath` option if it is defined, else it is relative to the location of `pannellum.htm`. An absolute URL can also be used.
`path`           | This is a format string for the location of the multiresolution tiles, relative to `multiRes.basePath`, which is relative to `basePath`. Format parameters are `%l` for the zoom level, `%s` for the cube face, `%x` for the x index, and `%y` for the y index. For each tile, `.extension` is appended.
`fallbackPath`   | This is a format string for the location of the fallback tiles for the CSS 3D transform-based renderer if the WebGL renderer is not supported, relative to `multiRes.basePath`, which is relative to `basePath`. The only format parameter is `%s`, for the cube face. For each face, `.extension` is appended.
`extension`      | Specifies the tiles' file extension. Do not include the `.`.
`tileResolution` | This specifies the size in pixels of each image tile.
`maxLevel`       | This specifies the maximum zoom level.
`cubeResolution` | This specifies the size in pixels of the full resolution cube faces the image tiles were created from.



### Video specific options

Currently, only equirectangular videos are supported.

Attribute        | Default | Description
-----------------|---------|-------------------------------------------
`video`          | `false` | The panorama is considered a video when this is set to `true`.
`panoramas`      |         | This parameter's value contains an array of objects designating the equirectangular video in various formats. Each object has a `file` property that contains the video's URL and a `type` property that contains the video's MIME type. Pannellum attempts to use video files in the order they are specified, so preferred formats should be placed first. An error is displayed if the user's browser does not support any of the specified formats. This parameter only has an effect is `video` is set to `true`.



## Additional information for tour configuration files

A tour configuration file contains two top level properties, `default` and
`scenes`. The `default` property contains options that are used for each scene,
but options specified for individual scenes override these options. The
`default` property is required to have a `firstScene` property that contains
the scene ID for the first scene to be displayed. The `scenes` property
contains a dictionary of scenes, specified by scene IDs. The values assigned to
these IDs are specific to each scene.
