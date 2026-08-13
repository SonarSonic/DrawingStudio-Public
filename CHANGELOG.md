## [v1.1.3-alpha] - 2026-08-13
### Added:
- Added: 3rd Party License Page, to credit Open Source libraries used to create Artrinth

### Fixed
- Fixed: Additional fixes for node sizing growing infinitely when using non-default scaling on Windows
- Fixed: Shape Fill node not rendering any fill when using input from the Shape Generator

## [v1.1.2-alpha] - 2026-08-08
### Added:
- Added: Support for editing Node parameters in the inspector

### Fixed
- Fixed: Inconsistent selection when clicking node sockets with a check-box
- Fixed: Page Layout window inconsistently failing to update its preset 
- Fixed: Node sizing growing infinitely when using non-default scaling on Windows
- Fixed: Memory leak retaining Image Resources after they're no longer needed
- Fixed: Noise Generation OpenGL shader not loading shader resources properly

## [v1.1.1-alpha] - 2026-08-03
### Added:
- Added: New revamped Drawing Synthesis nodes 
  - 'Letters Encoder', 'Dashes Encoder', 'Delaunay Triangulation', 'Minimum Spanning Tree', 'TSP Encoder', 'Quad Tile Encoder'
- Added: New Masking/Occlusion operation nodes
  - 'Hidden Line Removal' node for removing lines which are hidden / occluded behind other elements
  - 'Boolean Operation' node, for creating merged shapes / drawings, with enhanced support for shape or drawing inputs
  - 'Apply Mask' node for applying masks to shapes / drawings, to clip their contents
- Added: New 'Find Intersection Points' for finding points of intersection between two shapes or drawings
- Added: New spiral shape type 'Fermat'

### Changed
- Changed: Simplified transform controls for Image / Shape elements, allowed user auto-layout on all elements by default
- Changed: Renamed AutoLayout options, Scale to fit -> 'Fit', Crop to fit -> 'Fill', Stretch to fit -> 'Stretch'
- Changed: Merged all separate spiral shapes into a single spiral shape with sub-types for the different spiral types
- Changed: Standardized all shapes to use a center point as their position parameter
- Changed: Allow simultaneously editing the same element from the Node Graph, Inspector, Viewport Area, data parameters in the Node Graph will always take priority.
- Changed: Added support for saving input scenes with the project
- Changed: Added support for Undo/Redo with Image Elements
- Changed: Nodes which accept any element type now display as gray when no element is connected
- Changed: Nodes which expect a primary element type will display it, but still accept alternative elements if provided
- Changed: Maintain a per-workspace inspectable element in the Inspector
- Changed: Improved viewport / data parameter related modifications, bound data parameters will remain locked in the viewport
- Changed: The default color of Point elements + nodes
- Improved: Reduced memory usage from loading copies of the same image in different threads

### Fixed
- Fixed: Exports / Renders containing duplicate paths for shapes without fills
- Fixed: Noise Generation: OpenGL Noise Shader not loading properly and producing no output
- Fixed: Image created in the Compose workspace not keeping their transforms when rendered in nodes
- Fixed: Import Image showing no preview / not syncing transformation from the viewport to its settings
- Fixed: Shape Generator not syncing viewport modifications back to the node
- Fixed: Nested settings inside other nested settings not applying properly
- Fixed: Particle System / Contours / Edge Detection / Image Segmentation not clipping generated images to the bounds of the drawing
- Fixed: Particle System not respecting image bounds when translated
- Fixed: Check boxes appearing left justified in some situations in the node editor
- Fixed: Vector parameters not syncing individual components when they are bound to Node Links
- Fixed: Zero-length lines/segments not being drawn in the viewport/exports
- Fixed: Project display names appearing blank or overwritten when reopening existing projects
- Fixed: Viewer not updating when Show Node Previews is disabled
- Fixed: Tool Distribution not running with non-drawing inputs
- Fixed: Pinned node not being restored properly on project reload
- Fixed: Pinned node not being released when deleted.
- Fixed: Repeat node not rendering any output
- Fixed: Runnable nodes not being automatically triggered when switching to 'Automatic' execution mode
- Fixed: Auto-link not prioritizing primary sockets when creating links
- Fixed: Creating versions in Version Control & version control window corrupting window layout
- Fixed: Node's clipping their controls if they exceed the default width
- Fixed: Drawing importer incorrectly clipping nested SVG elements with viewports applied in
- Fixed: Drawing importer incorrectly scaling stroked path widths
- Fixed: Prevent Vulkan loading on platforms where no supported GPU is available

## [v1.1.0-alpha] - 2026-07-23
Drawing Studio is now Artrinth!
### Added
- Added: Additional example projects 'Kaleidoscope Contour', 'Image Contour', 'Voronoi Fill', 'Image Edges Style'
- Added: Workspaces, the default workspaces are 'Compose', 'Nodes' and 'Output'
  - These workspaces each contain a customisable window layout setup for streamlining different steps in the design process
  - 'Compose' - for configuring page layout / input layers
  - 'Nodes' - for designing the graphs, nodes, viewing the graph structure + node viewport area
  - 'Output' - for applying processing on the output design e.g. tool/color selection, export
- Added: Automatic / Manual execution modes for the Node Graph
  - Automatic: Nodes will re-process when parameters are changed, nodes don't require triggers to run.
  - Manual: Nodes require a trigger pulse or active trigger to run when a parameter is changed.
  - Switching between the modes is non-destructive, but trigger links, sockets will be hidden in Automatic mode, nodes which explicitly require manual mode will display a warning.
  - Most features can be used in Automatic mode, without needing to create trigger links.
- Added: Graph Runtimes - Overhauled internal Node Graph APIs to seperate graph structure from graph state and execution
  - Graphs can now be run in separate runtimes/threads, each with their own context window / data inputs
  - Allowing for highly advanced graphs, which process in parallel and share data between graphs
  - As well as allowing for future support of advanced features like sub graphs / compound nodes / creating custom processing pipelines
  - Features making the most of this feature will come in later updates, this was a large overhaul of the internal node graph and rendering system to be thread safe.
- Added: Graph Input / Outputs
  - Graphs now provide inputs + outputs parameters which are pinned to the side of the graph window
  - At the moment the data is pre-setup with the input scene + output scene by default
  - The graph inputs + output can be unpinned also and moved around like ordinary nodes
  - - Also related to future improvements for creating custom processing pipelines.
- Added: Primary Inputs + Outputs
  - Nodes now feature primary inputs, which are displayed above normal parameters
  - Primary inputs are typically the data required for the node to operate and are typically 'scene' or 'image' inputs only.
- Added: Inspector Window
  - A powerful general purpose way of editing properties on the currently selected element, primarily designed for scene elements in the 'Compose'
  - Also provides search functionality for finding properties on complex elements
- Added: Version Control Window
  - Allows for saving + restoring project versions, with support for naming, rating, notes similar to DBV3
- Added: Input Layers Window
  - Allows for viewing the current input layers, e.g. source images, SVGs, mask etc.
  - Allows for simple operations like selection, deletion, duplication etc.
- Added: Ability to switch node graphs from the node graph window
- Added: Dithering Algorithms, available in the new 'Image Stippler' + 'Dither' Nodes
  - Currently supported dithering methods: Floyd-Steinberg, Sierra, Sierra 2-row, Sierra Lite, Stucki, Atkinson, Burkes, Jarvis-Judice-Nicke, False-Floyd
- Added: Point Generation Node
  - Different methods of generating points, current methods 'Random', 'Poisson', 'Spiral', 'Uniform' and 'Concentric'
  - These nodes work great in combination with geometry generation nodes such as Voronoi Diagram
- Added: Geodesic Distance Node
  - Implements methods for calculating Geodesic Distance from an image, with seed points
  - The implementation uses a hybrid approach to the Fast Marching Method
  - Works well when combined with the new Contour Detection Node!
- Added: Contour Detection Node
  - Add support for detecting levels of contours in a source image
  - Uses a simple Marching Squares method
- Added: New GPU Renderer backends Vulkan (Windows + Linux only), Metal (macOS only).
  - Significant viewport performance improvements over the original OpenGL implementation
  - The new renderers are now the default on their supported platforms.
  - Available for viewport / preview / image export
  - OpenGL will continue to be supported. 
- Added: New Fill Types: Digital Fill, Inset Fill Type
  - Digital Fill: Overrides typical fill behaviour and is a purely digital fill to simplify creation of digital art.
  - Inset Fill: Fills shapes with a series of concentric shapes with customisable spacing
- Added: New Stroke Types: Solid, Default, Multi-Stroke, Dashed, None
- Added: Apply Stroke Node, for selecting different stroke types and applying to the input scene / elements.
- Added: Support for changing the color of frames/group elements
- Added: Support for opening project files at application startup
- Added: Support for scene-wide drawing distribution allows arbitrarily created shapes to also be assigned tools automatically
- Added: Reintroduced Drawing Tool Search tools
- Added: Additional undo/redo support, for node value changes / node color changes / drawing tool modifications
- Added: Support for loading legacy project drawings (.drawingbotv3)
- Added: Right-click menu to sockets showing available actions.
- Added: Right-click options for Reset / Randomise values on all nodes
- Added: Ability to create Node Links without dragging, by clicking once on the source socket and once on the destination socket.

### Changed
- Overhauled: Redesigned user interface controls + styling.
- Overhauled: Node now feature primary input / outputs.
- Overhauled: Improved interoperability of nodes, most nodes will now accept any 'scene' data types but may leave some data unprocessed.
- Overhauled: Merged Drawing/Image variants of Viewer/Import/Export into single nodes.
- Overhauled: Improved speed and reliability of SVG Import + support for additional svg element types 
- Improved: Reliability of clicking links in the graph area
- Improved: Reorganised node categories to simplify finding related nodes
- Improved: Moved Pinned/Viewed node to the viewport header.
- Improved: Added additional Image Metadata to Image data overlays, to display resolution, bit-depth
- Improved: Standardized padding / spacing across the UI
- Improved: Speed of Image Importer + Exporters, by using a clearer multi-threaded approach and switching to a faster native implementation.
- Improved: Support for importing 16-bit + 32-bit images without a loss in bit depth
- Improved: Added 'New' release status labels to new nodes
- Behavior: Use existing preset editor in Preset Manager when creating new presets
- Behavior: Open the main window as maximised on first launch by default
- Changed: Renamed some older windows, 'Search Nodes' is now 'Node Library'


### Fixed
- Fixed: Issue where nodes may flicker when first added to the graph, or one drag creating multiple nodes
- Fixed: Bug where selecting links might fail if they overlapped a frame.
- Fixed: Hide graph socket pop-ups when opening another menu / window
- Fixed: Font section on LBG Letters PFM node
- Fixed: Projects not re-opening properly after closing and re-opening
- Fixed: String option settings not appearing properly
- Fixed: PFMs not displaying in their category in the node selector
- Fixed: Transform node not affecting output
- Fixed: Shape node not restoring default settings properly
- Fixed: Frames sizing not updating when child nodes are removed
- Fixed: Viewport displaying previous project when closed
- Fixed: Point Encoders which don't output individual coordinates
- Fixed: Windows flickering when updating / saving the layout
- Fixed: Voronoi PFMs creating excessively high density plots + failing to complete
- Fixed: Mosaic PFMs not execution or failing to complete
- Fixed: Image segmentation executing additional unnecessary iterations
- Fixed: Colour sampling in Streamline based PFMs, fixes luminance based Tool Distributions
- Fixed: Close All Projects + Close Project not always functioning properly
- Fixed: PFMs creating reference images exceeding the platforms maximum resolution.
- Fixed: Drawings containing groups rendering incorrectly
- Fixed: macOS Delete key behavior, always use 'Delete' as the default and not 'Backspace'
- Fixed: Tone mapping not initalization properly for Adaptive PFMs
- Fixed: Viewport configuration not saving with individual projects
- Fixed: Node progress bars staying in a active state after node failure
- Fixed: Selection order of nodes in the viewport not respecting render order
- Fixed: Resizing controls not working properly if shift is pressed before first interation
- Fixed: Focus on selections in viewport being lost during rapid mouse movement.

## [v1.0.18-alpha] - 2026-04-20
### Added
- Added: Shape Fill Node for creating filled geometry shapes, supported fills: Hatch Fill, Pattern Fill (Lines, Crosshatch, Grid, Concentric Circles, Spiral, Zig Zag, Brick, Waves, Scales)
- Added: Additional Spiral shape types, Linear, Logarithmic & Parabolic.
- Added: Export Queue window, currently shows running export tasks and individual file progress, full export queuing functional is W.I.P.

### Changed
- Improved: Support for rendering PFMLayers / CMYK Separation while generating in the Viewport
- Improved: Improved the performance of the Viewport Renderer by supporting 'Volatile Path Rendering', resulting in smoother rendering while using Sketch PFMs
- Improved: Enhanced slider behavior, when dragging out of the visible range the slider will expand instead of clamping the value.
- Improved: Window Layout will now be saved / restored with the project, configurable in preferences
- Improved: Huge improvements
- Changed: All nodes now use MILLIMETRES as their default unit of measurement, except PFM / Encoders which still use PIXEL for consistency with DBV3

### Fixed
- Fixed: Mosaic PFMs support for CMYK separation
- Fixed: Changing color separation mode affecting all drawing sets
- Fixed: Application crashing when attempting to modify a shape while the PFM is processing
- Fixed: Page Layout presets not applying properly
- Fixed: User interface becomes unresponsive to user actions after prelonged use
- Fixed: Global penWidth not being applied to Drawing Sets
- Fixed: Page Color in the Page Setup being wiped when reloading projects
- Fixed: Node settings not appearing on repeater, position encoders, shape encoders
- Fixed: Shape encoder nodes not running properly
- Fixed: Application not responding or crashing when using extremely narrow / wide drawing areas
- Fixed: Short lines not displaying in the render output
- Fixed: Voronoi Diagram not running when passed 0 points
- Fixed: Multiple scaling/sizing issues on various nodes
- Fixed: Selecting specific Pens/Tools on a node might not restore properly
- Many more minor fixes and improvements


## [v1.0.17-alpha] - 2026-04-10
### Added
- Added: Support for saving/restoring custom window layouts, via Window/Layouts
- Added: Added experimental builds for Linux on aarch64

### Changed
- Drawing Studio now uses Java 26
- Improved: Added support for ganging on Vector controls
- Improved: Added support for switching between individual components / vector on vector controls
- Improved: Styling of Alpha/Beta labels on nodes
- Improved: Standardized using three decimal places for all setting/value types

### Fixed
- Fixed: CMYK Separation failing to complete
- Fixed: Linux installer crashing with nothing provides 'ocl-icd-opencl-dev'
- Fixed: Presets in PFM nodes not applying properly
- Fixed: Controls in the Preference window not shrinking when resizing the window
- Fixed: Missing preferences for HPGL / GCode configs
- Fixed: Expressions will now be evaluated properly for each iteration
- Fixed: Expressions being wiped when trying to modify them, in some situations
- Fixed: Expressions not being saved across nodes
- Fixed: Expressions not evaluating all number types properly
- Fixed: Allow entering values beyond 0-100% in the Viewport Zoom field
- Fixed: Application crashing when loading script nodes

## [v1.0.16-alpha] - 2026-03-19
### Added
- Added: 'Blend Factor' to Image Merger node

### Changed
- Overhaul: Complete rewrite of internal Setting API
- Overhaul: Huge internal refactoring, rewrites, reorganization of codebase
- Improved: UI Layout and Styling tweaks
- Improved: Re-designed PFM Controls style
- Improved: Design of Graph window to have borderless edges

### Fixes
- Fixed: Allowed editing of 'Drawing Styles' in Mosaic PFMs

## [v1.0.15-alpha] - 2025-12-09

### Changed
- Improved: Improved performance of the viewport renderer
- Improved: Added support for using the macOS Menu Bar which can be configured from User Interface preferences
- Overhaul: Redesigned internal unit testing frameworks

### Fixes
- Fixed: Application not starting properly on macOS
- Fixed: String/Text values not being editable after being entered
- Fixed: Integer values not being updated properly when using the slider, or text input
- Fixed: Path fill-rule not being respected by the Viewport Renderer
- Fixed: Nested alpha / blend modes not being interpretted properly in the SVG Importer
- Fixed: Edge cases where the SVG Importer would fail to render the SVG.

## [v1.0.14-alpha] - 2025-11-06
### Added
- Added: 'Hidden Line Removal' node for simplifying drawings, based on closed shapes
- Added: 'Apply Tool Distribution' node for applying a tool distribution to a drawing
- Added: 'Sawtooth Scribbler' node for applying a scribbled sawtooth pattern to an existing shape
- Added: 'Data Converter' node for quickly converting between data types
- Added: Notifications Panel, to keep track of recent actions and errors
- Added: Node Warnings, display errors and warnings above nodes, with suggested actions
- Added: Project tab selection to the top of the window

### Changed
- Drawing Studio now uses Java 25
- Improved: Visual design of Notification Pop-Ups, and unified notification icon and layout
- Improved: Allow selecting elements in the viewport within the bounds of the current element
- Improved: Accuracy of shape selection in the viewport, especially when zoomed out
- Improved: General UI layout / styling / spacing improvements

### Fixes
- Fixed: Viewport renderer not responding when drawing shapes with negative scaling
- Fixed: Nodes being deselected after dragging
- Fixed: Nodes failing silently and appearing to process successfully in certain situations
- Fixed: List node not outputting updated data when the list size is modified
- Fixed: Particle System generating two separate paths for reversed particles
- Fixed: Application crashing while modifying path during drawing generation
- Fixed: Streamlines PFMs not providing color sample information for Pen Distributions
- Fixed: PFMs exceeding the bounds of the provided image
- Fixed: Projects glitching being when opening two projects from the same source

## [v1.0.13-alpha] - 2025-10-22
### Added
- Added: 'SVG Importer' node for importing SVG files
- Added: 'Repeat Along Shape' + 'Repeat Along Line' nodes for creating repeating patterns
- Added: New Tool Distribution mode 'Ordered' for creating simple alternating patterns
- Added: Config option to 'Enable OpenGL Noise Generator Shader' which is disabled by default for better support of older hardware

### Changed
- Improved: Added previews to Align Node
- Improved: Unlocking the selected node will switch the viewer to the current node if one is selected
- Improved: Selecting a nodes view icon will now switch the viewed node only, and not lock the selection

### Fixes
- Fixed: Video Exports not encoding properly
- Fixed: Animation / Sequence exporter not rendering trimmed path segments
- Fixed: Animation / Sequence exporter ignoring the end-hold frame options
- Fixed: 'Superformula' shapes including invalid start point
- Fixed: Viewport selections failing due to invalid element bounds

## [v1.0.12-alpha] - 2025-10-10
### Added
- Added: New Shape Types Spiral, Cross, Superellipse and Superformula

### Changed
- Improved: Allow providing points for Shape positions
- Improved: Show only supported Viewport Anti-Aliasing Modes
- Improved: LBG PFMs speed between iterations
- Improved: UI Responsiveness during while a PFM is processing
- Improved: Automatically re-process nodes which depend on the Default Page Layout
- Overhaul: Migrated internal PFMs to new Shapes API
- Overhaul: Re-designed Hatch Fill algorithm to use a more efficient algorithm

### Fixes
- Fixed: Graph node not being restored after being minimized
- Fixed: Windows displaying resizing cursor after being redocked
- Fixed: Graph node glitching when being undocked from the window
- Fixed: Elements in the viewport not being selectable when switching nodes in complex rendering situations
- Fixed: Image Exporter displaying File Formats incorrectly
- Fixed: Stippling / Point Elements not outputting in SVG / Vector exports
- Fixed: Viewport rulers displaying the incorrect scale
- Fixed: Color Selection drop-down on Nodes cutting off the custom color label
- Fixed: Voronoi / Triangulation nodes exceeding the clipping bounds
- Fixed: Viewport Renderer not appearing when the GPU doesn't support MSAA
- Fixed: Remove MSAA Anti-Aliasing options on all integrated Intel GPUs

## [v1.0.11-alpha] - 2025-09-28

### Changed
- Improved: Accuracy of Voronoi Tree, Voronoi Triangulation + Voronoi TSP
- Improved: Render performance for complex path shapes
- Improved: Allow providing point lists for Spline and Polyline shapes

### Fixes
- Fixed: Node Data not being restored properly when reopening projects and copying nodes
- Fixed: List node not reloading additional created inputs
- Fixed: Heart shapes not applying position correctly
- Fixed: Points not being rendered at certain zoom levels with MSAA enabled.
- Fixed: Grid encoder not displaying any output
- Fixed: Pinned node control displaying incorrectly when switching projects

## [v1.0.10-alpha] - 2025-09-12

### Added
- Added: New 'Align' node for applying Horizontal + Vertical alignment to images, drawings and points.
- Added: Node Render Previews, to Draw Points, Random Points, Grid Points, Voronoi Diagram + all shape encoder nodes.

### Fixes
- Fixed: Images being cropped incorrectly when using PFMs
- Fixed: Viewer flickering when switching between some nodes
- Fixed: Drawing Exporter Node not completing properly
- Fixed: Circular Scribbler Node not completing properly
- Fixed: Particle System + Voronoi Diagrams + other shape encoders generating shapes which exceed the clipping bounds.
- Fixed: Path length calculations causing the application to freeze when using Sketch Quad Beziers

## [v1.0.9-alpha] - 2025-09-05

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

## [v1.0.8-alpha] - 2025-05-15

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

## [v1.0.7-alpha] - 2025-05-03
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

## [v1.0.6-alpha] - 2025-01-24

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

## [v1.0.5-alpha] - 2025-01-15

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

## [v1.0.4-alpha] - 2025-01-10

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

## [v1.0.3-alpha] - 2025-01-03

### Changed
- Improved Geometry Clipping performance

### Fixed
- Application not loading on macOS x86 systems - [#1](https://github.com/SonarSonic/DrawingStudio-Public/issues/1)
- Fixed GPU Renderer not loading on low powered GPUs

## [v1.0.2-alpha] - 2023-11-29

## [v1.0.1-alpha] - 2023-10-30

## [v1.0.0-alpha] - 2023-08-30


