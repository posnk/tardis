In order to implement a new widget for the "tardis" panel one has to provide at
least:
 * An empty paint method to override the WTK default paint-background method
 * A create-widget fucntion that sets w_mode and instantiates a WTK widget with
   a correctly set width field.

An example widget implementation is provided below:


    #include <stdlib.h>
    
    #include <cairo.h>
    
    #include <wtk/widget.h>
    
    #include "tardis.h"

    /* Paint method, called whenever the widget needs to be updated */
    void example_paint(wtk_widget_t *w, cairo_t *context, int focused)
    {
    }
    
    /* Process method, called periodically by the panel application, use this for *
     * dynamic content */
    void example_process(panel_widget_t *w)
    {
    }
    
    /* Creation method */
    panel_widget_t *example_create()
    {
    	/* Specify the width of the widget, the other fields are set by the *
    	 * panel layout routine */
    	clara_rect_t rect = {0, 0, 200, 0};
    
    	/* Allocate memory for the widget object */
    	panel_widget_t *w = malloc(sizeof(panel_widget_t));
    
    	/* This is a fixed width widget */
    	w->w_mode = PANEL_W_MODE_FIXED;
    
    	/* Instantiate the WTK widget */
    	w->widget = wtk_create_widget(rect);
    
    	/* Set the callbacks */
    	w->widget->callbacks.paint = &example_paint;
    	w->process = &example_process;
    
    	/* Optionally, set the implementation specific data pointer */
    	w->impl = NULL;
    	return w;
    }


