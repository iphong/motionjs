motion.js
======

A rich Javascript 3D Transform & Animation library based entirely on CSS3

EXAMPLES:
    
    // Time unit is default to 'ms' and distance unit is default to 'px'
    
    // Basic Transforms
    motion("#selector").translateZ(100).scale(0.5);
    motion("#selector").pivot("left).rotateY(45);
    motion("#selector").perspective(500);
    
    // Simple animations
    motion("#selector").transition("all",500).translateY(200);
    motion("#selector").animate(500, "translateY", 200);
    
    // Complex keyframed and stacked animation chain

    // Keyframing
    motion("#selector")
        .animation()
        .start(fn)  // do something before animation start
        .set(500, "translateY", 200)
        .set(1000, "rotateY", 45)
        .set(2000, function() { this.scale(0.5).translateZ(40).rotateX(10); })
        .set(2500, function() { this.reset(); })
        .end(function bar() {
            // Animation completed.
        });

    // Stacking
    motion("#selector")
        .animation()
        .delay(500)
        .start("opacity", 0.5)  // set default state before animation start
        .next(100, "scaleX", 1.3)
        .next(150, "scaleX", 0.7)
        .next(150, "translateZ", 300)
        .end(function() {
            // you can continue to create another animation stack
            this.animate(500, "rotateX", 30).after(500, function() {
                // It's finally end
            });
        });

// BETA FEATURES

3D Viewport Class

var viewport = new motion.Viewport({ perspective: 500 });


3D Box Class Constructor

var floor = new motion.Box(200,10,200).in(viewport);

// create a new 3d box and makes it a child of floor
var box1 = new motion.Box({ width: 40, height: 40, depth: 40 }).parent(floor);

// create an exact version of box1 and append to its location
var box2 = box1.clone(); 

// create new box instance like box2, but don't append it to the DOM yet
var box3 = new motion.Box({ height: 60 }).similar(box2);

// Create a proxy version of box3, this instance has its own transform channels, 
// but any other properties remain sync with the original instance, unless defined.
var box4 = box3.proxy();







