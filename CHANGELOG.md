## [1.0.9] - 2025-09-05

### Added
- Added: Node Render Previews, nodes will display a small preview of their output to help speed up workflows
- Added: New Noise Types: OpenSimplex2, OpenSimplex2S, Perlin, Cellular, Value Cubic, Value
- Added: New Fractal noise options: allows combining octaves of noise layers
- Added: New Tool Distribution mode 'Color Similarity' an alternative faster approach to Color Match with higher accuracy but more pen lifts, it can be weighted by Lightness Bias / Chroma Bias / Hue Bias.
- Added: New Blend Modes: Hue, Saturation, Color and Luminosity
- Added: New 'Simplify Dashes Strokes' option to SVG Export, to simplify strokes using 'dash-array' and 'dash-offset' attributes for easy plotting
- Added: New Canny Edge Detection - GPU Accelerated Image filter
- Added: New Shape Types Line, Circle, Rounded Rectangle, Quad Curve, Cubic Curve, Arc, Heart, Polyline, Catmull-Rom Spline, Path, SVG Path
- Added: Position, Vertices, Shapes, Distance and Render Time to the viewport area
- Added: Support for Blend Modes in SVG export
- Added: Support for exporting Images + Shapes in SVG/PDF
- Added: Support for trackpad Zoom & Scroll gestures in the Viewport & Graph
- Added: Exported Inkscape SVGs will now display the pen color as the layer/label color
- Added: Support for Custom Transformation for Images & Shapes and improved Layout / Alignment controls
- Added: Display the current viewed node above the viewport, with clearer view lock button.

### Improved
- Improved: Complete re-write + re-design of Mask / Shape editing controls
- Improved: Complete re-write of Export API, allows for faster export and using the GPU for fast image export.
- Improved: Re-designed the User Interface to use a more modern design, clearer separation of windows
- Improved: Switched to GPU based Noise Algorithms, allowing for much faster noise generation, if the GPU initialization fails the CPU fallback will be used.
- Improved: Reduced memory consumption during typical usage
- Improved: Reduced idle CPU Usage
- Improved: Performance improvements to UI update speed / responsiveness
- Improved: Performance improvements to image transfers between different render frameworks via shared native buffers
- Improved: Speed / Performance of SVG Export
- Improved: Particle System node at high velocities, improved curve support
- Improved: Speed of Image to Image node transfers
- Improved: Speed / Quality of Image Exports when using the legacy CPU renderer
- Improved: Render performance when rendering large amounts of points
- Improved: Masking is now Stroke-Aware, more accurate and faster especially with Cubic Curves + Quad Curves
- Improved: Redesigned Drawing Pen Setup window design
- Overhaul: Rewritten Mask / Vector Editing overlays to use faster rendering pipeline

### Changes
- Changed: Removed the 'Classic' viewport renderer
- Changed: Standardised Node labels, icons and color.
- Changed: Renamed 'Process Folder' to 'Watch Folder'
- Changed: You now press Ctrl or Command to zoom in the viewport / graph or use a Zoom Gesture on Trackpad
- Removed: Experimental / Broken nodes - Start Workflow, Finish Workflow, Hilbert Curve, Create Tool
- Removed: Broken legacy DrawingBotV3 nodes.
- Removed: 'Viewport Renderer' and 'Render Quality' options
- Removed: Unsupported Geometry Filter parameters

### Fixed
- Fixed: Streamlines PFMs not updating the progress bar properly
- Fixed: Merging drawings containing the same drawing set
- Fixed: Memory leak caused by PFM tasks not being disposed of properly while displayed in the viewport
- Fixed: Issue where dragging nodes into the graph may stutter and create multiple instances
- Fixed: 'Create List' & 'Create Ranged List' becoming empty / glitched when the data type is changed
- Fixed: TreeViews in the Node Selector / Graph Inspector / Project Manager displaying de-selected elements as still highlighted
- Many more fixes and improvements

### Notes
- Project Manager database is not stable and will be replaced with a new system in the future
- Many nodes are still experimental, and some designs / layouts are not complete

## [1.0.8] - 2025-05-15

### Changed
- Drawing Studio now uses Java 24

### Fixed
- Fixed: Application not starting on macOS / other devices which don't support Anti-Aliasing
- Fixed: Fallback to Anti-Aliasing OFF when not supported
- Fixed: Editing text values in Colour Picker dialog when out of range
- Fixed: Validate user-input in Page Layout controls to prevent negative/invalid inputs
- Fixed: Hovering over data sockets containing Point2D not showing a data preview
- Fixed: Image Analysis nodes not running on macOS
- Fixed: CMYK Alignment with drawings with margins
- Fixed: Classic Renderer not drawing / freezing the UI
- Fixed: LBG PFMs not clearing the canvas after each iteration
- Fixed: CMYK not displaying preview while the drawing is being generated

## [1.0.7] - 2025-05-03
macOS: DrawingStudio now requires macOS 11+

### Added
- Added: Boolean Operation node for merging two shape elements with the following modes available: Difference, Intersect, Union, XOR, Reverse Difference
- Added: Additional 25+ maths functions
- Added: Ability to customise the Stroke Attributes + Fill Attributes for individual drawing pens
- Added: Ability to merge drawings with different pens selected
- Added: Visibility icons to Drawing Pens to allow quick toggling of displayed pens, without affecting export/distribution
- Added: Rescale Quality to Page Layout controls
- Added: DPI + Anti-Aliasing inputs to Rasterize Drawing

### Changed
- Drawing Studio now uses Java 21
- Overhauled viewport renderer for faster rendering / better multi-threading performance
- Overhauled user interface layout allowing for better customisation of tool window size, position and location.
- Re-designed colour selection pop-up windows
- Added new pen/tool selection window
- Merged 'Simplex Noise XY' + 'Simplex Noise XYZ' into new node called 'Simplex Noise'
- Merged individual 'Split Image' / 'Merge Image' nodes for individual colour separations in two new nodes 'Split Channels' + 'Merge Channels'
- Internally switched to new localisation system to allow local language translations in the future
- Overhauled all internal serialization / deserialization
- Improved viewport loading time on start-up
- Complete re-design and re-write of many internal systems including new Element API, Attribute API, Shape API, Tool API, Editor API, Setting API, Registry API and Data API
- Note: Removed simple-sketch-style example project, more example projects will be added once the API has stabilised

### Fixed
- Fixed: Nodes processing multiple times when two data inputs are changed in quick succession
- Fixed: Nodes not updating if a range slider is dragged out of range
- Fixed: Node colors not updating in the Graph Inspector
- Fixed: Viewport freezing when a node is deleted
- Fixed: Data Collector, data count not updating properly
- Fixed: Trigger Sender/Receiver not connecting properly, not sharing colour information
- Fixed: Trigger Buffer, not responding when connections are added and removed
- Fixed: Trigger Gate / Conditional Gate not removing sockets/connections when a NOT gate is used

### Note
- Large portions of the codebase have been completed re-designed overhauled so expect more instability/bugs, it also breaks compatibility projects from previous versions
- Multiple features are also currently broken / not complete, including workflows, scripting and CLI

## [1.0.6] - 2025-01-24

### Added
- Added 'Process Folder' - for automatically processing folders of files and reacting to changes
- Added 'Data Collector' - allowing data to be collected into lists for further processing
- Added 4 GPU-Accelerated Image Filters - Difference of Gaussians (DoF), Ridge Filter, Bilateral Filter, Edge-Preserving Smoothing

### Changed
- Added ability to cycle through lists of images in the 'Display Image' node
- Display folder names in a smaller font and shorten the path when the value is too long
- Pressing 'Center' on any empty graph will now move the graph back to X 0, Y 0
- Added accepted Data Types / Formats when hovering over data sockets
- Added Page Layout output to 'Import Image' node

### Fixed
- Fixed multiple project reloading issues
- Fixed Data Connector & Trigger Connector not loading properly
- Nodes not being able to be deleted by the user when data is not serializable
- Importing projects failing if serialized data is invalid
- When dragged Data Connectors / Data Viewers / Transform nodes will now auto-connect through their sockets
- Fixed 'Shape' node not switching between shape types
- Fixed Position Encoders which require Tone Mapping generating invalid results
- Fixed Python Integration not loading required native libraries
- Fixed viewport sizing not reflecting image dimensions properly when switching between images of different sizes
- Fixed simple sketch example project not opening

## [1.0.5] - 2025-01-15
 
### Added
- Added 'Data Switch' node to switch between two data inputs
- Added 'Rotate' to Transform Node
- Added 'Orientation' to Page Layout node
- Added 'Width' + 'Height' output and 'Page Rescaling' controls to Import Image node
- Added File/Export Displayed Image - to allow quick export of the current image in the viewport

### Changed
- Page Layout Node will now update units + ganged values
- Improved performance when resizing the viewport

### Fixed
- Node graph glitching when deleting nodes while they are being viewed
- Selections not being removed properly in certain situations
- Image Filter / Drawing Style options not saving
- PFM, Image and Math nodes not updating after type changed
- Image Filters not showing the result if the type is changed while selected
- Graph inspector becoming unusable after an unexpected Undo/Redo operation
- Node Blocks not creating blocks when dragged
- Import Image: Not updating when Rotation / Flip Settings are changed
- Transform Node: Skews not being applied from the anchor point
- Page Layout Node not loading the users default preset on creation
- Merge Drawings + Export Drawing showing no preview in the viewport 
- Original Colour pen when using Sketch Sweeping Curves
- Simple sketch example project not opening

## [1.0.4] - 2025-01-10

### Added
- New 'Trigger Connector' Node: for re-routing trigger links
- Transform Node: Added ability to transform Drawings, 2D Points, 3D Points
- Pulse animation to links and sockets when data is changed
- Added inputs to 'Option' settings, which can be a number or text

### Changed
- Overhauled internal Graph + Data API, to support more flexible data transfer
- Improved data transfer speeds + general processing performance
- Renamed many nodes with simpler names
- Added additional sub-menus to Path Finding Modules + Image Filters

### Fixed
- Transform Node: Fixed issues detecting the data input
- Node labels not being saved/reloaded 
- Right/Left arrow keys not working within nodes using text areas
- Projects not loading when Node types are removed
- Trigger sockets not staying highlighted for the same duration as links
- GPU Renderer causing applicaton crash when Drawing Area width/height is set to 0
- Conditional + Trigger Gates not saving their Gate Type
- Option style settings not saving properly

## [1.0.3] - 2025-01-03

### Changed
- Improved Geometry Clipping performance

### Fixed
- Application not loading on macOS x86 systems - [#1](https://github.com/SonarSonic/DrawingStudio-Public/issues/1)
- Fixed GPU Renderer not loading on low powered GPUs

## [1.0.2] - 2023-11-29

## [1.0.1] - 2023-10-30

## [1.0.0] - 2023-08-30


