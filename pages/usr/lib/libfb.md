# libfb
A simple framebuffer library

## Types
* The actual framebuffer object.
    ```c
    typedef struct {
        int fd;
        uint8_t *fbmem;       /* mapped framebuffer */
        size_t screensize;
        unsigned width;
        unsigned height;
        unsigned bpp;
        unsigned line_length;

        /* optional software back buffer */
        uint8_t *backbuf;
    } fb_t;
    ```
* A colour object. Effectively a tuple
    ```c
    typedef struct {
        uint8_t r, g, b;
    } color_t;
    ```

## Functions
* Initialises a framebuffer object.
    ```c
    fb_t fb_init(void);
    ```
* Opens a framebuffer device into the object
    ```c
    int fb_open(fb_t *fb, const char *dev);
    ```
* Closes the framebuffer device and unmaps memory
    ```c
    void fb_close(fb_t *fb);
    ```
### Drawing Primitives
* Clears the screen
    ```c
    void fb_clear(const fb_t *fb, color_t c);
    ```
* Draws a pixel at the specified coordinate
    ```c
    void fb_putpixel(const fb_t *fb, unsigned x, unsigned y, color_t c);
    ```
* Draws a horizontal line
    ```c
    void fb_hline(const fb_t *fb, unsigned x, unsigned y, unsigned w, color_t c);
    ```
* Draws a vertical line
    ```c
    void fb_vline(const fb_t *fb, unsigned x, unsigned y, unsigned h, color_t c);
    ```
* Draws a filled rectangle
    ```c
    void fb_fillrect(const fb_t *fb, unsigned x, unsigned y, unsigned w, unsigned h, color_t c);
    ```
* Draws a rectangle outline
    ```c
    void fb_fillrect(const fb_t *fb, unsigned x, unsigned y, unsigned w, unsigned h, color_t c);
    ```
* Draws a line between 2 points
    ```c
    void fb_line(const fb_t *fb, int x0, int y0, int x1, int y1, color_t c);
    ```
* Draws a single character
    ```c
    void fb_draw_char(const fb_t *fb, unsigned x, unsigned y,
                  char ch, color_t fg, color_t bg);
    ```
* Draws a string
    ```c
    void fb_draw_string(const fb_t *fb, unsigned x, unsigned y,
                    const char *str, color_t fg, color_t bg);
    ```
* Flips the back and the front buffer
    ```c
    void fb_flip(const fb_t* fb);
    ```

## Macros
* Creates a colour object
    ```c
    #define COLOR(r,g,b) ((color_t){(r),(g),(b)})
    ```
* Creates a colour object using a preset
    ```c
    #define COLOR_BLACK  COLOR(0,0,0)
    #define COLOR_WHITE  COLOR(255,255,255)
    #define COLOR_RED    COLOR(255,0,0)
    #define COLOR_GREEN  COLOR(0,255,0)
    #define COLOR_BLUE   COLOR(0,0,255)
    ```