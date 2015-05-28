---
title: Control the Drawing Order in Cocos2d and Sprite Kit neatly
slug: control-drawing-order-cocos2d-spritekit
gamernews_id: 368
---            

In both Cocos2d and Sprite Kit the drawing order of your Nodes is primarily determined by the hierarchy of your scenes - children are drawn on top of their parents. In many games you will need to change this drawing order manually, for example to force UI elements to be drawn on top of all other Nodes.

Cocos2d and Sprite Kit both provide a z-Value on Nodes to determine a manual ordering.

In Cocos2d the property on CCNode is called **zOrder**. In Sprite Kit it is the **zPosition**.

In Cocos2d Nodes with a lower value are drawn on the topmost layer, in Sprite Kit the Nodes with the highest value are drawn on the top.

Most developers end up choosing arbitrary values for zOrder/zPosition (*-1000, 200)* but there is a much neater way to solve this - **using an enum**! Here is an example *DrawingOrder.h* file that you can include in your project:

    //  DrawingOrder.h

    #ifndef DeepMine_DrawingOrder_h
    #define DeepMine_DrawingOrder_h

    // example for Sprite Kit, for Cocos2d simply inverse the order of the values!
    typedef NS_ENUM(NSInteger, DrawingOrder) {
      DrawingOrderBackground,
      DrawingOrderMineLayers,
      DrawingOrderElevator,
      DrawingOrderWorkers,
      DrawingOrderUIElements
    };

    #endif

Instead of assigning arbitrary values, you add all different z-levels to an enum. Every enum entry represents a Integer number. *DrawingOrderBackground* corresponds to *0*, *DrawingOrderMineLayers* corresponds to *1*, etc. 

This is a much nicer way to keep track of different z-levels. You can easily add or remove layers and change their order.

Once you place this header file in your project you can include it in any Node where you need to set a manual z-level:

**Sprite Kit**

    #import "DrawingOrder.h"
    ...
    worker.zPosition = DrawingOrderWorkers;

**Cocos2d**

    #import "DrawingOrder.h"
    ...
    worker.zOrder = DrawingOrderWorkers;

Happy coding!

benji@makeschool.com
