#  Storyboard VS Programmic UI

## Notes:

1. When you drag a `UIView` from a storyboard to your `UIViewController` to create an outlet in iOS development, you typically choose `strong` under the storage type for the outlet. This is because of how memory management is handled in Objective-C and Swift with ARC (Automatic Reference Counting).

Here’s why you generally use `strong` for these outlets:

1. **Ownership and Memory Management**: By default, outlets should be `strong` because the view controller needs to own the view. This ownership implies that as long as the view controller is alive, its views should also remain in memory unless explicitly set to nil. The `strong` keyword ensures that the view is kept in the memory as long as its view controller exists by creating a strong reference to it.

2. **View Lifespan**: Views in a view controller's hierarchy are usually essential for the view controller's functionality. If these views were referenced weakly, they could be deallocated while the view controller is still using them, leading to potential crashes due to dangling pointers.

3. **Interface Builder and Strong References**: When you use Interface Builder (the storyboard), the views you add are inherently retained strongly by their parent view. Since the view controller's main view retains its subviews strongly, your outlet should also be strong to align with this behavior unless there's a specific reason to avoid a strong reference cycle.

### When to Use Weak
You might use `weak` in situations where you are dealing with potential retain cycles, especially with delegate relationships or closures/blocks that might capture `self` (the view controller) strongly. For views, it’s less common to need weak references, but one typical case is when you have an IBOutlet that might not always be part of the view hierarchy, like an optional view that could be removed from its superview at runtime.

Overall, using `strong` for UIView outlets in a UIViewController is standard practice to ensure that these objects are properly retained as long as they are needed.


2. To check whether an outlet is strong or weak after it has been created in your iOS project, you can look at the property declaration in your Swift or Objective-C code. Here's how you can confirm the memory management attribute for each language:

### In Swift
In Swift, if you used Interface Builder to drag a `UIView` to a `UIViewController` and create an outlet, you can find the corresponding property in your view controller’s `.swift` file. Look for the property declaration:

- **Strong (Default)**: If the property does not explicitly say `weak`, then it is strong by default. Swift uses strong references for class instances unless specified otherwise.
  
  ```swift
  @IBOutlet var myView: UIView!
  ```

- **Weak**: If the property is weak, it will be marked with the `weak` keyword.
  
  ```swift
  @IBOutlet weak var myView: UIView?
  ```

### In Objective-C
In Objective-C, you need to check the property attributes in the header (.h) file or the implementation (.m) file of your view controller:

- **Strong**: The property will be marked with `strong` or `retain` (in older code) in the property declaration.
  
  ```objc
  @property (strong, nonatomic) UIView *myView;
  ```

- **Weak**: The property will include the `weak` attribute.
  
  ```objc
  @property (weak, nonatomic) IBOutlet UIView *myView;
  ```

### Verifying in Interface Builder
You can also verify the strength of a reference in Xcode’s Interface Builder:

1. Open the storyboard or XIB file.
2. Select the view controller that contains the outlet.
3. Open the Connections Inspector (right panel, rightmost tab).
4. Look at the “Referencing Outlets” section. If you hover over the outlet connection, it won’t explicitly tell you if it's strong or weak, but you can right-click on the view controller’s dock (the small circle below the view controller in the storyboard scene) to see all connections. It shows each IBOutlet along with its property declaration (`weak` if set).

By checking these sections of your code and Interface Builder, you can determine if an outlet is strong or weak. Remember, unless specified as `weak`, outlets are strong by default in Swift, and need to be explicitly declared as `strong` or `retain` in Objective-C.

3. Do not Repeat Cod Yourself

For example, we can use outlet collections.


4. call super method when you overwrite a function 
