Quick Protocol Overview
----

1. Export a complete, joined design to dxf file
2. Convert with linkCad
3. Upload design to uPG software
3. Load wafer ready to be exposed
4. Expose

CAD design
---
The design must have no overlapping lines. The best way to check for this is to make sure that everything joins properly. You can also select and delete parts of the design to see if any stray lines are hidden under your design.

You do not want to have any borders or outlines that are a single line (such as wafer boundaries). The uPG will print everything starting at the outermost line.

Center your design. The X-Y origin should be the center of your design.

The uPG passes over the entire area of the design regardless of whether there are gaps between areas. It writes vertical lines (y-direction) and then moves over one position in the x direction. The time your design takes to write depends on how many vertical lines the uPG needs to scan. So it is best to align your designs to take up the least amount of space in the x-direction.

For example, B M L takes more time the BML, but both of these examples would take at least 3 times more write time as:

B

M

Ｌ

Conversion with LinkCAD
----
The uPG software cannot see features within features. It exposes everything inside the outermost line. LinkCad tricks the uPG into printing features within features by cleverly cutting design into smaller separate adjacent parts. 

1. Save your design as a dxf formatted file.
2. Open linkCad. Leave the import and export formats as DXF. Note: dxf format has no scale information so it asks you to enter it. Give it whatever scale you are using in your dwg file. Typically 1 unit = 1 mm. Scale 1 times. Set the exports units the same.
3. Browse to and import your dxf file.
4. Typically you will have a number of open polygons. Check "join adjacent open polygons" and "Close open polygons" and click repair.
5. Click view at the top of the screen, and turn fill on (it looks like a "%" sign in the tool bar) to help visualize what will be exposed. Areas that are to be exposed are filled in with gray. You'll notice that features within features are filled in twice. We will fix that in the next step.
6. Go to Tools > De-Embed Polygons. Depending on the geometry of you design on option may work better. Usually "Cut-line in re-entrant polygons" works.
7. Now you should see the preview with you design in gray with no double exposed areas. If it doesn't look right most likely there is an un-joined or overlapping line in your original design. Problem areas are usually highlighted with a triangle.
8. Go back to the convert tab and click next. A few open remaining polygons are OK as long as the preview looked good.
9. Click next again and save the converted dxf. It's best to use a new file name indicating that it is converted.


Converting Designs with Arrays
---

If you design includes any array it is usually too complex for the De-embed polygon function. For arrays you will add it as a second file during the conversion process.

1. Save the array separately from the main design. You must insure that the array lines up with the main design. The easiest way to do this is to create the whole design with the array and save as two different files. Then delete the array in one file, and everything but the array in the second file.
1. Proceed as above with the main file (minus arrays). After you De-Embed polygons you will subtract the array from the first file.
1. Go to Tools > Boolean Operations on Files.
1. Select the array as "File (B)". The select A minus B (subtract). Leave Explode cells checked. The precision can be 10 nm or lower.
1. Your array should be successfully cut out from the design. 
1. If your array contains a large number of elements the preview may freeze when you try to zoom in to check. You can check a small portion by using the window-drawing-zoom option rather than incrementally zooming in. The to return click the zoom to full image option. You should see the array elements in white (if they are intended to be pillars) and cuts going out. 

Setting up the uPG for exposure
----
You will want to have a wafer ready with SU-8, softbakeing.

1. Turn on the compressor and vacuum pump.
1. Start the uPG exposure wizard software and load the design. If you used 1 unit = 1 mm in the LinkCAD conversion then you want to scale by 1000000.
1. The preview is useless. Don't worry if there is a large black filled in part. What is important to check is the overall design dimensions. This is the actual size that it will print as. Compare them to your design. If they are off something was scaled wrong. Also check the centering. A few microns off is OK but if there is a significant offset it may print off the wafer.
1. Click show control panel and click 'To Load' in the resulting window. 
1. Get your wafer ready by using a razor to scrape off any SU-8 from the bottom or use a moist kimwipe with acetone and clean the bottom and then blow off any debris.
1. Use the aligning pins to center the wafer on the stage and turn on the vacuum with the blue switch.
1. Remove the aligning pins and click 'To Center'. Next click focus.
1. Exposure settings depend on the thickness of your SU-8. The highest energy for one pass is 18 MW at 99% strength and 4X time. If your SU-8 is 20 micrometer one pass at these settings should be good. For small features ( less than 15um), unidirectional mode should have a check mark. If your design is taller or shorter you will need to run multiple passes or increase the speed (3x 2x or 1x) or decrease exposure energy. You can tell if your design is over exposed if the surface of the cured SU-8 has a cracked appearance. SU-8 under 20 micrometers also has a good chance of peeling away when it is developed. One solution for this is to do a post-post exposure bake at 120C before developing. Another option is to spin and cure a thin layer of SU-8 (like SU-8 2002 @ 2000 rpm) on the wafer before spinning the design layer. This helps the design layer adhere.
1. Expose X number of times (use team-viewer to run again remotely).

Multi-Layer Masters
-----
1. expose the first layer as above, align the wafer with the pins in a way that you can place it again on the stage in approximately the same way. Usually you can place the of the corners of straight edges at a pin.
1. Complementary alignment marks must be added to each layer of the design. Place the distinct feature of the alignment marks at an integer coordinate as it is easier to type in later. Alignment marks placed at 12 O'clock, and 6 O'clock will not add any write time for the design.
1. Use the advanced alignment with the exposure wizard. 
1. Check the mark1 and mark2 and enter the coordinates of the distinct feature
1. A green cross-hairs will appear with a live camera image of the wafer. If you were lucky enough to place the wafer in close to the same position than you should see you alignment mark. Move the stage or the cross-hairs to the location that corresponds to the coordinates and click the middle mouse button(scroll wheel)
1. You will be prompted to do the same for the second alignment mark.
1. Finally it will give you a report telling you how much it will compensate for re-alignment. If these numbers seem odd you may have switch alignment marks.

Masters of around 10 um in height and smaller have a special issues with alignment because total internal reflection causes the marks to be invisible through the camera (you’re not crazy). The solution is to selectively wash away the SU-8 around the alignment mark. Take a q-tip sponge and wet it with developer. The carefully wash away the SU-8 from around the alignment mark. You must place the alignment mark far enough away from the design so that you avoid washing away areas of the design.

Checklist
----
- [ ] Is the design joined with no overlapping lines or wafer outlines?
- [ ] Do the dimensions in the preview of the uPG make sense?
- [ ] Did you scrape SU-8 off the back of the wafer before loading?
- [ ] Did you remove the alignment pins after you loaded the wafer?
- [ ] Is team-viewer running if a second exposure is needed?
