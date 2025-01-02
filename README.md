# Image Selection & Projective Editing Tool

This project is a **Java Swing application** for interactively selecting regions in an image and performing various operations—such as intelligent “scissor” selections, filling, deleting, **pasting** external images in perspective, and adding **projective text**. The tool supports multiple “selection models,” including:

- **Point-to-Point**: Connect corners manually in a simple line-by-line approach.  
- **Intelligent Scissors**: Use gradient-based pathfinding to select regions with minimal “edge cost.”  
- **Projective Text**: Click four corners to define a quadrilateral, then warp text (or an external image) into that shape for a perspective effect.

## Features

1. **Image Loading & Saving**  
   - Open images in PNG, JPEG, or other supported formats.  
   - Save *selected regions* to a PNG (with transparency around the region).

2. **Selection Models**  
   - **PointToPointSelectionModel**: basic line segments between clicked points.  
   - **ScissorsSelectionModel**: “intelligent scissors” that find edges based on image gradients.  
   - **ProjectiveTextSelectionModel** (or a variant): specifically expects 4 clicks for a quadrilateral, enabling projective warping.

3. **Operations on Selected Regions**  
   - **Fill** with a color.  
   - **Delete** (clear) the region from the image.  
   - **Paste** another image (optionally in perspective) into the selection.  
   - **Add Perspective Text**: type in text, which is rendered and warped into the selected quadrilateral.

4. **Undo/Redo (Optional)**  
   - Single-step backups can be handled by storing a copy of the image pre-operation.  

5. **GUI Features**  
   - **Control Panel**: Buttons for Undo, Reset, Finish, Delete, Fill, Projective Text, etc.  
   - **Menus**: File operations (Open, Save, Close) and Edit operations (Undo, Delete, Fill with Color, Projective Paste).  
   - **Interactive** image panel with mouse listeners for selection, plus real-time feedback.

---

## Setup & Requirements

- **Java** 17+ (or a recent Java version).
- **Swing** is included in the standard library; no extra GUI framework needed.
- **Optional**: If you want advanced interpolation (like `warpPerspective` from OpenCV), you’d need OpenCV for Java. But the default code works with plain Java2D.

### Building

1. **Clone** or download the repository:
   ```bash
   git clone https://github.com/YourUsername/YourRepo.git
   cd YourRepo
   ```
2. **Compile** using your preferred method:
   - **Maven** or **Gradle** (if you’ve set up a build file), or  
   - **IDE** (IntelliJ/Eclipse/VSCode) by importing the project as a Java project.

3. **Run** the main class, e.g.:
   ```bash
   # if there's a build script that produces a jar
   java -jar build/libs/YourRepo.jar
   # or via IDE "Run" on class selector.SelectorApp
   ```

---

## Usage Guide

1. **Starting the App**  
   - Launch `selector.SelectorApp` to open the main window.
2. **Open an Image**  
   - File → Open...  
   - Choose a local file (PNG/JPG).  
3. **Choose a Selection Model**  
   - Use the dropdown (or combobox) on the right panel to pick:  
     - *Point-to-point*,  
     - *Intelligent scissors*,  
     - or a *Projective* mode (if you added that option).
4. **Select**  
   - Click around the image to create segments.  
   - If using the projective model, you must click exactly **4 corners** (the shape will auto-finish after the 4th).
5. **Finish**  
   - Click **Finish** (or middle-click, depending on your setup) to close the polygon.  
   - The **selection** is now in a `SELECTED` state.
6. **Operations**  
   - **Fill**: “Fill with Color” → pick a color.  
   - **Delete**: “Delete Selected Region” → clears region to transparency.  
   - **Paste** in Perspective: 
     1. Choose “Paste Image...” from the menu or a button.  
     2. Load an external image.  
     3. The image is warped into your 4-corner selection.  
   - **Projective Text**: Type text and color → it’s warped into the selected quadrilateral.
7. **Save**  
   - File → Save... to export the *selected region* as a separate PNG with transparency.  
   - Or do a normal screenshot if you want the entire window state.

---

## Advanced Topics

- **Homography**  
  - The projective warp is computed by solving a 3×3 matrix from the source rectangle `(0,0..w,h)` to user-defined corners.
- **Alpha Blending**  
  - Overlays (e.g. text, pasted images) can be combined with existing pixels using custom blending code in `warpImage(...)`.
- **Intelligent Scissors**  
  - Uses gradient-based edge costs to automatically find the “least-cost path” between points in the image.

---

## Contributing

Feel free to **open an issue** or **submit a pull request** if you:

- Find bugs or have suggestions.
- Want to improve the warp interpolation or alpha blending.
- Have new ideas for selection models or image transforms.

---

## License

This project is distributed under [MIT License](LICENSE) (or whichever you prefer).  
See the **LICENSE** file for more details.

---

## Acknowledgments

- [OpenCV](https://opencv.org/) for advanced perspective warping examples (optional).
- Various resources on “Intelligent Scissors” and gradient-based image segmentation.
- Java & Swing for the built-in 2D graphics library.

---

**Enjoy** using the “Image Selection & Projective Editing Tool”! For questions or support, please open an issue on GitHub or contact the maintainers.
