## Precursor
[__Follow Apple coding practices!__](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.pdf)
 
A short list of highlights from Apple's guidelines:

  * Prefix all classes, protocols, functions, constants and typedef (don't prefix methods)
  * All `BOOL` types should be prefixed with a verb (can, shows, is, has, should, ..)
  * Methods that an action should start with a verb (except use "do" which rarely adds meaning).
  * All methods names should include descriptive word(s) before an argument.  
  
    ```objc
    - (BOOL)tableView:(NSTableView *)tableView shouldSelectRow:(int)row;
    ```
  * Delegate methods should start with the class that is sending the message.  
  
    ```objc
    - (id)viewWithTag:(NSInteger)aTag; //Right.
    - (id)taggedView:(int)aTag;        //Wrong.
    ```
  * Never use blank keywords in method names.  
  
    ```objc
    - (int)runModalForDirectory:(NSString *)path 
                           file:(NSString *)name 
                          types:(NSArray *)fileTypes; //Right.
    - (int)runModal:(id)path :(id)name :(id)type;     //Wrong.
    ```
  * When declaring @properties and ivars, line up the variable names vertically.
  * Long method/function names are ok and should have line breaks after the colon.
  * The format for custom notification names is:  
  
    ```objc
    //[Name of associated class] + [Did | Will] + [UniquePartOfName] + Notification
    extern NSString *NSApplicationDidBecomeActiveNotification;
    ```
  * Private ivars should be prefixed with the underscore
  * Prefer defining categories inline in the header file instead of separate .h/.m file (external categories tend to get lost in the code base).

## Best Practices

 * __Use self-documenting code where ever possible!__ (Prefer frequent and explicit variable names over comments inside functions.)
 * __Always use ARC!__
 * Understand [memory management](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MemoryMgmt/MemoryMgmt.pdf) even if you're using ARC. 
 * Always access properties with `self.` (unless inside it's own setter/getter).
 * Warning are errors that haven't broken yet.
 * Understand [KVO/KVC](http://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/KeyValueObserving/KeyValueObserving.pdf), [Notification Center](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Notifications/Notifications.pdf), Delegates and [Blocks (aka closures in other languages)](http://developer.apple.com/library/ios/documentation/cocoa/Conceptual/Blocks/Blocks.pdf) for communicating between objects.
 * Your code isn't fit to be used unless you've tested on a phyical device and checked performance/leaks with Instruments.
 * Break coding tasking into something that can be completed in 1 to 4 hours. Commit and sync code base at least once a day.

## Layout

 * Use spaces, not tabs.
 * 4 spaces for indentation.
 * A line of code should not be more than 90 characters (preferences > Text Editing to turn on page guide)

## Documentation

 * Comments should be hard-wrapped at 90 characters.
 * Documentation and/or sample code should be at the top of the interface file(.h).


## Declarations

 * Always declare memory-management semantics even on `readonly` properties.
 * Always use `@synthesize`. Prefer letting private ivars be implicit.  
 * Pointer notations `*` must have a single space before and no space afterwards.  
 * Methods with similar functionality should be grouped together using inline categories with an explicit name for its purpose. (Avoid `#pragma mark`) 
 * constants should be grouped by their corresponding inline category.
  
    ```objc
    @interface UIView(UIViewHierarchy)
    @property(nonatomic,readonly) UIView       *superview;
    @property(nonatomic,readonly,copy) NSArray *subviews;
    
    - (void)removeFromSuperview;
    ...
    @end 
    
    UIKIT_EXTERN const CGSize UILayoutFittingCompressedSize NS_AVAILABLE_IOS(6_0);
    UIKIT_EXTERN const CGSize UILayoutFittingExpandedSize NS_AVAILABLE_IOS(6_0);
    
    @interface UIView (UIConstraintBasedLayoutFittingSize)
    ...
    ```
  * Private methods and properties must be defined in an empty category at the top of the implementation file(.m).  
  
    ```objc
    //.m
    @interface MyClass()
  
    @property(nonatomic, retain) BOOL *showView;
  
    @end
    ```

## Control Structures

 * Always surround `if` bodies with curly braces, unless breaking or returning.
 * All curly braces should begin and end on a new line (including blocks).
 * Put a single space after keywords and before their parentheses.
 * Return and break early.
 * No spaces between parentheses and their contents.
  
    ```objc
    if (hasError)
        return;

    if (something == nil)
    {
        // do stuff
    }
    else
    {
        // do other stuff
    }
    ```
 * Any conditional checking that involves more than one check must be captured in a variable.   
 
    ```objc
    BOOL isStuffNotAThing = (stuff != thing && [stuff isKindOfClass:[thing class]]);
    if (isStuffNotAThing)
        return error;
    ```

## Blocks

 * Blocks should have a space between their return type and name.
 * Block definitions should include their return type when possible.
  
    ```objc
    void (^blockName1)() = ^()
    {
        // do some things
    };

    MyObj (^blockName2)(MyObj *obj, MyObj *obj2) = ^MyObj (obj, obj2)
    {
        // do some things
    };
    ```
 * Blocks used as a parameter for a completion of an asynchronous function should be defined in the header.
 * Asynchronous methods should include the final argument as a block named "completion:" and have a typedef block name.
  
    ```objc
    extern typedef void(^RGASyncFinished)(NSSet* modifiedCheckins, NSError* error);
 
    - (void)synchronizeCheckins:(NSSet*)checkins
                     completion:(RGASyncFinished)callback;
    ```

## Literals

 * Always use object literals. (`@String`, `@1`, `@[@1,@2,@3]`,`@{key:@value}`)
 * Avoid multiple subscripting calls in the same line.
 * Unless being used as a parameter, the contents of array and dictionary literals should be on new lines.
 * Dictionary literals should have no space between the key and the colon, and a single space between colon and value.  
  
    ``` objc
    NSArray *numbers = @[
        @1,
        @2,
        @3
    ];

    NSDictionary *keyedDcitionary = @{
        GHDidCreateStyleGuide: @YES
    };

    [anObject doSomethingWithThis: @[@"Hello", @"World"]];
    ```


## Categories

 * Categories should be named for the sort of functionality they provide. Don't create umbrella categories.
 * Category methods should always be prefixed.
 * If you need to expose private methods for subclasses or unit testing, create a class extension named `Class+Private`.


## Interface Builder

 * Use Interface Builder where ever possible, as it is much easier to maintain and adapt than code.
 * Break up storyboards into logical sections to avoid large merge conflicts. 
 * `IBAction` should be named in a reactionary fashion.
  
    ``` objc
    - (IBAction)theButtonWasPressed:(id)sender;
    ```

## Constants

 * Never use magic numbers. (Exceptions include multiplying by 1, -1, and 0.)
 * When possible, establish constants using the `const` keyword. Expose them when appropriate with the `extern` keyword.
 
    ``` objc
    const float half = 2.0f;
    float totalWidth = outerView.frame.size.width;
    float innerWidth = innerView.frame.size.width;
    float centerXAxis = (innerWidth / half) - (totalWidth / half);
    ```
 * `extern` and `const` should be favored over `#define`
 
    ``` objc
    extern const NSString *RGAImageDidChangeNotification = @"RGAImageDidChangeNotification";  //Right
    #define RGAImageDidChangeNotification @"RGAImageDidChangeNotification";                   //Wrong
    ```

