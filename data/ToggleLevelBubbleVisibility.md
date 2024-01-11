/*
Toggle the visibility of the Level Bubble in Section/Elevation
The snippet can be reused for Grids
TESTED REVIT API: 2018
The snippet can be used as is in a Revit Application Macro for test purposes
Author: Deyan Nenov | github.com/ArchilizerLtd
This file is shared on www.revitapidocs.com
For more information visit http://github.com/gtalarico/revitapidocs
License: http://github.com/gtalarico/revitapidocs/blob/master/LICENSE.md
*/

public void ToggleLevelBubbles()
{
    Document doc = this.ActiveUIDocument.Document;
    Selection sel = this.ActiveUIDocument.Selection;

    do
    {
      //Pick the Level you want to toggle in Elevation/Section
      Level lvl = doc.GetElement(sel.PickObject(ObjectType.Element, "Pick View to Align To")) as Level;

      using(Transaction t = new Transaction(doc, "toggle"))
      {
        t.Start();
        lvl.HideBubbleInView(DatumEnds.End0,doc.ActiveView);  //DatumEnds.End1 to toggle the other End
        t.Commit();
      }				
    }
    while(true);
}