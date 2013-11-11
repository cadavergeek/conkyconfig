--==============================================================================
--  conky_time.lua
--  author  : Cadaver
--  version : 20131010
--  license : Distributed under the terms of GNU GPL version 2 or later
--
--  conky_grey_cai.lua
--  author  : CAI
--  version : 20130509
--  license : Distributed under the terms of GNU GPL version 2 or later
--
--  original conky_grey.lua
--  author  : SLK
--  version : v2011062101
--  license : Distributed under the terms of GNU GPL version 2 or later
--
--  analog clock algorythm
--  author  : ramzport (http://ramzport.blogspot.ru/2012/04/conkylua-1.html)
--==============================================================================

require 'cairo'

--------------------------------------------------------------------------------
--                                                                    clock DATA

function go_clock()
  if conky_window == nil then return end
  local cs = cairo_xlib_surface_create(conky_window.display, conky_window.drawable, conky_window.visual, conky_window.width, conky_window.height)
  cr = cairo_create(cs)

  local nXCenter = conky_window.width/2
  local nYCenter = 80
  local nRadius = conky_window.width/2 - 10

  local nSecond = tonumber(os.date('%S'))
  local nMinute = tonumber(os.date('%M'))
  local nHour = tonumber(os.date('%I'))
  if nHour == 12 then nHour=0 end

  --CLOCK

  --shadow
  cairo_set_source_rgba(cr, fRGBtoARGB(0x000000, 0.3))
  cairo_new_sub_path(cr)
  cairo_arc (cr, nXCenter+1, nYCenter+1, nRadius, math.rad(0), math.rad(360))
  cairo_fill(cr)

  --clock face
  cairo_set_source_rgba(cr, fRGBtoARGB(0xffffff, 1))
  cairo_new_sub_path(cr)
  cairo_arc (cr, nXCenter, nYCenter, nRadius-2, math.rad(0), math.rad(360))

  local pLin = cairo_pattern_create_radial (nXCenter, nYCenter, 0, nXCenter, nYCenter, nRadius-5)
  cairo_pattern_add_color_stop_rgba (pLin, 0.0, fRGBtoARGB(0xffffff, 1))
  cairo_pattern_add_color_stop_rgba (pLin, 0.4, fRGBtoARGB(0xeeeeee, 1))
  cairo_pattern_add_color_stop_rgba (pLin, 1, fRGBtoARGB(0xcccccc, 1))
  cairo_set_source (cr, pLin)
  cairo_fill(cr)
  cairo_pattern_destroy (pLin)

  for i = 0, 12 do
    nTheta = math.rad(i*30)
    nXCoord = nXCenter + (nRadius-12)*math.cos(nTheta)
    nYCoord = nYCenter + (nRadius-12)*math.sin(nTheta)
    nXoCoord = nXCenter + (nRadius-4)*math.cos(nTheta)
    nYoCoord = nYCenter + (nRadius-4)*math.sin(nTheta)

    fLine(nXoCoord, nYoCoord, nXCoord, nYCoord, 0x000000, 1, 2)
  end

  for i = 0, 60 do
    nTheta = math.rad(i*6)
    nXCoord = nXCenter + (nRadius-9)*math.cos(nTheta)
    nYCoord = nYCenter + (nRadius-9)*math.sin(nTheta)
    nXoCoord = nXCenter + (nRadius-5)*math.cos(nTheta)
    nYoCoord = nYCenter + (nRadius-5)*math.sin(nTheta)

    fLine(nXoCoord, nYoCoord, nXCoord, nYCoord, 0x000000, 1, 1)
  end


  -- text on clock face
  fDrawTextCenter (nXCenter, nYCenter+30, 'Ubuntu', 'DejaVu Sans Condensed', 9, 0, 0, 0x555555, 1, 0)

  -- hour
  nTheta = math.rad(270+nHour*30+nMinute/2)
  nXCoord = nXCenter+(nRadius-27)*math.cos(nTheta)
  nYCoord = nYCenter+(nRadius-27)*math.sin(nTheta)
  nXoCoord = nXCenter-5*math.cos(nTheta)
  nYoCoord = nYCenter-5*math.sin(nTheta)

  fLine(nXoCoord+1, nYoCoord+1, nXCoord+2, nYCoord+2, 0x000000, 0.3, 5)

  cairo_set_line_width (cr, 5)
  cairo_set_source_rgba(cr, fRGBtoARGB(0x000000, 1))
  cairo_move_to(cr, nXoCoord, nYoCoord)
  cairo_line_to(cr, nXCoord, nYCoord)
  cairo_stroke(cr)

  nTheta = math.rad(270+nHour*30+nMinute/2)
  nXCoord = nXCenter+(nRadius-28)*math.cos(nTheta)
  nYCoord = nYCenter+(nRadius-28)*math.sin(nTheta)
  nXoCoord = nXCenter-4*math.cos(nTheta)
  nYoCoord = nYCenter-4*math.sin(nTheta)

  fLine(nXoCoord, nYoCoord, nXCoord, nYCoord, 0x555555, 1, 3)

  -- minute
  nTheta = math.rad(270+nMinute*6)
  nXCoord = nXCenter+(nRadius-17)*math.cos(nTheta)
  nYCoord = nYCenter+(nRadius-17)*math.sin(nTheta)
  nXoCoord = nXCenter-5*math.cos(nTheta)
  nYoCoord = nYCenter-5*math.sin(nTheta)

  fLine(nXoCoord+1, nYoCoord+1, nXCoord+2, nYCoord+2, 0x000000, 0.3, 4)

  cairo_set_line_width (cr, 4)
  cairo_set_source_rgba(cr, fRGBtoARGB(0x000000, 1))
  cairo_move_to(cr, nXoCoord, nYoCoord)
  cairo_line_to(cr, nXCoord, nYCoord)
  cairo_stroke(cr)

  nTheta = math.rad(270+nMinute*6)
  nXCoord = nXCenter+(nRadius-18)*math.cos(nTheta)
  nYCoord = nYCenter+(nRadius-18)*math.sin(nTheta)
  nXoCoord = nXCenter-4*math.cos(nTheta)
  nYoCoord = nYCenter-4*math.sin(nTheta)

  fLine(nXoCoord, nYoCoord, nXCoord, nYCoord, 0x555555, 1, 2)

  -- second
  nTheta = math.rad(270+nSecond*6)
  nXCoord = nXCenter+(nRadius-7)*math.cos(nTheta)
  nYCoord = nYCenter+(nRadius-7)*math.sin(nTheta)
  nXoCoord = nXCenter-10*math.cos(nTheta)
  nYoCoord = nYCenter-10*math.sin(nTheta)

  fLine(nXoCoord+1, nYoCoord+1, nXCoord+2, nYCoord+2, 0x000000, 0.3, 3)

  cairo_set_line_width (cr, 3)
  cairo_set_source_rgba(cr, fRGBtoARGB(0x000000, 1))
  cairo_move_to(cr, nXoCoord, nYoCoord)
  cairo_line_to(cr, nXCoord, nYCoord)
  cairo_stroke(cr)

  nTheta = math.rad(270+nSecond*6)
  nXCoord = nXCenter+(nRadius-8)*math.cos(nTheta)
  nYCoord = nYCenter+(nRadius-8)*math.sin(nTheta)
  nXoCoord = nXCenter-9*math.cos(nTheta)
  nYoCoord = nYCenter-9*math.sin(nTheta)

  fLine(nXoCoord, nYoCoord, nXCoord, nYCoord, 0xffffff, 1, 1)

  -- glossy
  cairo_set_source_rgba(cr, fRGBtoARGB(0xffffff, 1))
  cairo_new_sub_path(cr)
  cairo_arc (cr, nXCenter, nYCenter, nRadius, math.rad(0), math.rad(360))

  local pLin = cairo_pattern_create_radial (nXCenter, nYCenter-50, 0, nXCenter, nYCenter-50, nRadius+55)
  cairo_pattern_add_color_stop_rgba (pLin, 0.0, fRGBtoARGB(0xffffff, 0.4))
  cairo_pattern_add_color_stop_rgba (pLin, 0.3, fRGBtoARGB(0xffffff, 0.1))
  cairo_pattern_add_color_stop_rgba (pLin, 1, fRGBtoARGB(0xffffff, 0.0))
  cairo_set_source (cr, pLin)
  cairo_fill(cr)
  cairo_pattern_destroy (pLin)
end

function fRGBtoARGB (nColor, nAlpha)
  return ((nColor / 0x10000) % 0x100) / 255., ((nColor / 0x100) % 0x100) / 255., (nColor % 0x100) / 255., nAlpha
end

function fDrawTextCenter (nXCenter, nYCenter, sText, sFontName, sFontSize, nFontSlant, nFontWeight, nColor, nAlpha, nRotate)
  local extents = cairo_text_extents_t:create()
  cairo_select_font_face (cr, sFontName, nFontSlant, nFontWeight)
  cairo_set_font_size (cr, sFontSize)
  cairo_text_extents (cr, sText, extents)
  local nXSpace = nXCenter-(extents.width/2)
  local nYSpace = nYCenter
  cairo_move_to (cr, nXSpace, nYSpace)
  cairo_set_source_rgba(cr, fRGBtoARGB (nColor, nAlpha))
  cairo_rotate (cr, nRotate*math.pi/180)
  cairo_show_text(cr, sText)
  cairo_rotate (cr, (0-nRotate)*math.pi/180)
end

function fLine(nXoCoord, nYoCoord, nXCoord, nYCoord, nColor, nAlpha, nWidthLine)
  cairo_set_source_rgba(cr, fRGBtoARGB(nColor, nAlpha))
  cairo_set_line_width (cr, nWidthLine)
  cairo_move_to(cr, nXoCoord, nYoCoord)
  cairo_line_to(cr, nXCoord, nYCoord)
  cairo_stroke(cr)
end

-- HOURS
clock_h = {
    {
    name='time',                   arg='%H',                    max_value=12,
    x=80,                          y=90,
    graph_radius=63,
    graph_thickness=3,
    graph_unit_angle=30,           graph_unit_thickness=30,
    graph_bg_colour=0xffffff,      graph_bg_alpha=0.0,
    graph_fg_colour=0xFFFFFF,      graph_fg_alpha=0.3,
    txt_radius=44,
    txt_weight=1,                  txt_size=11.0,
    txt_fg_colour=0xFFFFFF,        txt_fg_alpha=0.6,
    graduation_radius=65,
    graduation_thickness=6,        graduation_mark_thickness=2,
    graduation_unit_angle=30,
    graduation_fg_colour=0xFFFFFF, graduation_fg_alpha=0.3,
    },
}
-- MINUTES
clock_m = {
    {
    name='time',                   arg='%M',                    max_value=60,
    x=80,                          y=90,
    graph_radius=67,
    graph_thickness=2,
    graph_unit_angle=6,            graph_unit_thickness=6,
    graph_bg_colour=0xffffff,      graph_bg_alpha=0.1,
    graph_fg_colour=0xFFFFFF,      graph_fg_alpha=0.3,
    txt_radius=80,
    txt_weight=0,                  txt_size=10.0,
    txt_fg_colour=0xFFFFFF,        txt_fg_alpha=0.6,
    graduation_radius=57,
    graduation_thickness=0,        graduation_mark_thickness=2,
    graduation_unit_angle=30,
    graduation_fg_colour=0xFFFFFF, graduation_fg_alpha=0.3,
    },
}
-- SECONDS
clock_s = {
    {
    name='time',                   arg='%S',                    max_value=60,
    x=80,                         y=90,
    graph_radius=60,
    graph_thickness=2,
    graph_unit_angle=6,            graph_unit_thickness=2,
    graph_bg_colour=0xffffff,      graph_bg_alpha=0.0,
    graph_fg_colour=0xFFFFFF,      graph_fg_alpha=0.2,
    txt_radius=50,
    txt_weight=0,                  txt_size=9.0,
    txt_fg_colour=0xFFFFFF,        txt_fg_alpha=0.3,
    graduation_radius=0,
    graduation_thickness=0,        graduation_mark_thickness=0,
    graduation_unit_angle=0,
    graduation_fg_colour=0xFFFFFF, graduation_fg_alpha=0.0,
    },
}

--------------------------------------------------------------------------------
-------------------------------------------------------------------------------
--                                                                 rgb_to_r_g_b
-- converts color in hexa to decimal
--
function rgb_to_r_g_b(colour, alpha)
    return ((colour / 0x10000) % 0x100) / 255., ((colour / 0x100) % 0x100) / 255., (colour % 0x100) / 255., alpha
end

-------------------------------------------------------------------------------
--                                                            angle_to_position
-- convert degree to rad and rotate (0 degree is top/north)
--
function angle_to_position(start_angle, current_angle)
    local pos = current_angle + start_angle
    return ( ( pos * (2 * math.pi / 360) ) - (math.pi / 2) )
end

-------------------------------------------------------------------------------
--                                                              draw_clock_ring
-- displays clock
--
function draw_clock_ring(display, data, value)
    local max_value = data['max_value']
    local x, y = data['x'], data['y']
    local graph_radius = data['graph_radius']
    local graph_thickness, graph_unit_thickness = data['graph_thickness'], data['graph_unit_thickness']
    local graph_unit_angle = data['graph_unit_angle']
    local graph_bg_colour, graph_bg_alpha = data['graph_bg_colour'], data['graph_bg_alpha']
    local graph_fg_colour, graph_fg_alpha = data['graph_fg_colour'], data['graph_fg_alpha']

    -- background ring
    cairo_arc(display, x, y, graph_radius, 0, 2 * math.pi)
    cairo_set_source_rgba(display, rgb_to_r_g_b(graph_bg_colour, graph_bg_alpha))
    cairo_set_line_width(display, graph_thickness)
    cairo_stroke(display)

    -- arc of value
    local val = (value % max_value)
    local i = 1
    while i <= val do
        cairo_arc(display, x, y, graph_radius,(  ((graph_unit_angle * i) - graph_unit_thickness)*(2*math.pi/360)  )-(math.pi/2),((graph_unit_angle * i) * (2*math.pi/360))-(math.pi/2))
        cairo_set_source_rgba(display,rgb_to_r_g_b(graph_fg_colour,graph_fg_alpha))
        cairo_stroke(display)
        i = i + 1
    end
    local angle = (graph_unit_angle * i) - graph_unit_thickness

    -- graduations marks
    local graduation_radius = data['graduation_radius']
    local graduation_thickness, graduation_mark_thickness = data['graduation_thickness'], data['graduation_mark_thickness']
    local graduation_unit_angle = data['graduation_unit_angle']
    local graduation_fg_colour, graduation_fg_alpha = data['graduation_fg_colour'], data['graduation_fg_alpha']
    if graduation_radius > 0 and graduation_thickness > 0 and graduation_unit_angle > 0 then
        local nb_graduation = 360 / graduation_unit_angle
        local i = 1
        while i <= nb_graduation do
            cairo_set_line_width(display, graduation_thickness)
            cairo_arc(display, x, y, graduation_radius, (((graduation_unit_angle * i)-(graduation_mark_thickness/2))*(2*math.pi/360))-(math.pi/2),(((graduation_unit_angle * i)+(graduation_mark_thickness/2))*(2*math.pi/360))-(math.pi/2))
            cairo_set_source_rgba(display,rgb_to_r_g_b(graduation_fg_colour,graduation_fg_alpha))
            cairo_stroke(display)
            cairo_set_line_width(display, graph_thickness)
            i = i + 1
        end
    end

    -- text
    local txt_radius = data['txt_radius']
    local txt_weight, txt_size = data['txt_weight'], data['txt_size']
    local txt_fg_colour, txt_fg_alpha = data['txt_fg_colour'], data['txt_fg_alpha']
    local movex = txt_radius * (math.cos((angle * 2 * math.pi / 360)-(math.pi/2)))
    local movey = txt_radius * (math.sin((angle * 2 * math.pi / 360)-(math.pi/2)))
    cairo_select_font_face (display, "ubuntu", CAIRO_FONT_SLANT_NORMAL, txt_weight);
    cairo_set_font_size (display, txt_size);
    cairo_set_source_rgba (display, rgb_to_r_g_b(txt_fg_colour, txt_fg_alpha));
    cairo_move_to (display, x + movex - (txt_size / 2), y + movey + 3);
    cairo_show_text (display, value);
    cairo_stroke (display);
end

-------------------------------------------------------------------------------
--                                                               go_clock_rings
-- loads data and displays clock
--
function go_clock_rings(display)
    local function load_clock_rings(display, data)
        local str, value = '', 0
        str = string.format('${%s %s}',data['name'], data['arg'])
        str = conky_parse(str)
        value = tonumber(str)
        draw_clock_ring(display, data, value)
    end
    
    for i in pairs(clock_h) do
        load_clock_rings(display, clock_h[i])
    end
    for i in pairs(clock_m) do
        load_clock_rings(display, clock_m[i])
    end
    for i in pairs(clock_s) do
        load_clock_rings(display, clock_s[i])
    end
end

-------------------------------------------------------------------------------
--                                                                         MAIN
function conky_main()
    if conky_window == nil then 
        return
    end

    local cs = cairo_xlib_surface_create(conky_window.display, conky_window.drawable, conky_window.visual, conky_window.width, conky_window.height)
    local display = cairo_create(cs)
    
    local updates = conky_parse('${updates}')
    update_num = tonumber(updates)
    
    if update_num > 5 then
-- Original conky_grey clock
        go_clock_rings(display)
-- Analog clock
--        go_clock()
--        go_gauge_rings(display)
    end
    
    cairo_surface_destroy(cs)
    cairo_destroy(display)
end

