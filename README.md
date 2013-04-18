These guidelines build on Apple's existing [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html).
Unless explicitly contradicted below, assume that all of Apple's guidelines apply as well.

_This styleguide is based on [GitHub's Objective-C conventions](https://github.com/github/objective-c-conventions), but we don't agree on everything :)_

## Whitespace
 
 * Indent blocks using 4 spaces
 * Activate "Automatically trim trailing whitespace" and "Including whitespace-only lines" in Xcode settings -> Text Editing.
 * Make liberal use of vertical whitespace to divide code into logical chunks.
 * Blocks are separated by one, and only one, empty line.

## Documentation and Organization

 * All method declarations should be documented using the [AppleDoc](github.com/tomaz/appledoc) standard.
 * Comments should be hard-wrapped at 80 characters.
 * Use `#pragma mark`s to categorize methods into functional groupings and protocol implementations, following this general structure:

    // -----------------------------------------------------------------------------
    #pragma mark - TABLE VIEW DELEGATE
    // -----------------------------------------------------------------------------

 * Use the same groupings in header files, but format them according as AppleDoc:

    /// ----------------------------------------------------------------------------
    /// @name Table View Delegate
    /// ----------------------------------------------------------------------------

## Declarations

 * Always prefer properties to ivars.
 * Prefer exposing an immutable type for a property if it being mutable is an implementation detail. This is a valid reason to declare an ivar for a property.
 * Don't use `@synthesize` unless the compiler requires it. Note that optional properties in protocols must be explicitly synthesized in order to exist.
 * Instance variables should be prefixed with an underscore (just like when implicitly synthesized).
 * Don't put a space between an object type and the protocol it conforms to.
 
    @property (attributes) id<Protocol> object;
 
 * C function declarations should have no space before the opening parenthesis, and should be namespaced just like a class.

    void NMAwesomeFunction(BOOL hasSomeArgs);

## Expressions

 * Don't access an ivar unless you're in `-init`, `-dealloc` or a custom accessor.
 * Use dot-syntax for getters, but not setters:
 
    [self.manager setDelegate:self];

 * Use object literals, boxed expressions, and subscripting over the older, grosser alternatives.
 * Comparisons should be explicit for everything except `BOOL`s.
 * Prefer positive comparisons to negative.
 * Long form ternary operators should be wrapped in parentheses and only used for assignment and arguments.

    Blah *a = (stuff == thing ? foo : bar);

 * Short form, `nil` coalescing ternary operators should avoid parentheses.

    Blah *b = thingThatCouldBeNil ?: defaultValue;

 * There shouldn't be a space between a cast and the variable being cast.

    NewType a = (NewType)b;

## Control Structures

 * Always surround `if` bodies with curly braces.
 * All curly braces should begin on the same line as their associated statement. They should end on a new line.
 * Else statements should begin on a new line.
 * Put a single space after keywords and before their parentheses.
 * Return and break early.
 * No spaces between parentheses and their contents.

    if (something == nil) {
	    // do stuff
    }
    else {
	    // do other stuff
    }

## Literals

 * Avoid making numbers a specific type unless necessary (for example, prefer `5` to `5.0`, and `5.3` to `5.3f`).
 * The contents of array and dictionary literals should have a space on both sides.
 * Dictionary literals should have no space between the key and the colon, and a single space between colon and value.

    NSArray *numbers = @[ @1, @2, @3 ];
    NSDictionary *prefs = @{ @"FollowConventions": @YES };

 * Longer or more complex literals should be split over multiple lines (and never have a terminating comma):

    NSArray *theShit = @[
        @"Lorem ipsum and stuff...",
        @"And the quick brown fox",
        @"They should be friends"
    ];

## Categories

 * Categories should be named for the sort of functionality they provide.