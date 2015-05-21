quick protocol overview
----

1. Export complete, joined design to dxf file
2. Convert with linkCad
3. Load design on to uPG
3. Load wafer ready to be exposed
4. Expose

CAD design
---
The design must have no overlapping lines. The best way to check for this is to make sure that everything is joins properly. You can also select and delete parts of the design to see if any stray lines are hidden under your design.

You do not want to have any borders or outlines that are a single line. The uPG will print everything starting at the out most line.

Center your design. The X-Y origin should be the center of your design.

Conversion with LinkCAD
----
The uPG software cannot see features within features. It exposes everything inside the outermost line. LinkCad tricks the uPG into printing features within features by cleverly cutting design into smaller separate parts. 

1. Save your design as a dxf formatted file.  
2. Open linkCad. Leave the import and export formats as DXF. Note: dxf format has no scale information so it asks you to enter it. Give it whatever scale you are using in your dwg file. Typically 1 unit = 1 mm. Scale 1 times. Set the exports units the same.
3. Browse to and import your dxf file.
4. Typically you will have a number of open polygons. Check "join adjacent open polygons" and "Close open polygons" and click repair.
5. Click view at the top of the screen, and turn fill on to help visualize what will be exposed. Areas that are to be exposed are filled in with grey. You'll notice that features within features are filled in twice. We will fix that in the next step.
6. Go to Tools > De-Embed Polygons. Depending on the geometry of you design on option may work better. Usually "Cut-line in re-entrant polygons" works.
7. Now you should see the preview with you design in grey with no double exposed areas. If it doesn't look right most likely there is an un-joined or overlapping line in your original design. Problem areas are usually highlighted with a triangle.
8. Go back to the convert tab and click next. A few open remaining polygons are ok as long as the preview looked good.
9. Click next again and save the converted dxf. It's best to use a new file name indicating that it is converted.


Converting Designs with Arrays
---

If you design includes any array it is usually to complex for the De-embed polygon option. For arrays you will add it as a second file during the conversion process.

1. Save the array separately from the main design. You must insure that the array lines up with the main design. The easiest way to do this is to create the whole design with the array and save as two different files. Then delete the array in one file, and everything but the array in the second file.
2. Proceed as above with the main file. After you De-Embed polygons you will add the array.
3. Go to Tools > Boolean Operations on Files.
4. Select the array as "File (B)". The select A minus B (subtract). Leave Explode cells checked. The precision can be 10 nm or lower.
5. Your array should be successfully cut out from the design. 
6. If your array contains a large number of elements the preview may freeze when you try to zoom in to check. You can check a small portion by zooming in away from the array and then panning over to it. You should see the array elements in white (if they are intended to be pillars) and cuts going out.

Setting up the uPG for exposure
----
You will want to have a wafer ready with SU-8 softbakeing.

1. turn on the compressor and vacuum pump.
2. Start the exposure wizard.
3. Load the design. If you used 1 unit = 1 mm in the LinkCAD conversion then you want to scale by 1000000.
4. The preview is useless. Don't worry if there is a large black filled in part. What is important to check is the overall design dimensions. This is the actual size that it will print as. Compare them to your design. If they are off something was scaled wrong. Also check the centering. A few microns off is ok but if there is a significant offset it may print off the wafer.
5. Exposure settings
6. Expose X number of times (use teamviewer to run again remotely)

Multi-Layer Masters
-----
1. expose the first layer as above, align the wafer with the pins in a way that you can place it again on the stage in approximately the same way. Usually you can place the of the corners of straight edges at a pin.
2. Complementary alignment marks must be added to each layer of the design. 



Checklist
----
- [ ] Is the design joined with no overlapping lines or wafer outlines?
- [ ] Do the dimensions in the preview of the uPG make sense?
- [ ] Did you scrape SU-8 off the back of the wafer before loading