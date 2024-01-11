/*
Make a selection of objects in view filtering by category 
This works just as Filter Selection but in Reverse. It allows you to first select the Category of the Selection by 
picking up an Object of that Category and follow up with a standard rectangular selection. After finishing the selection, only 
objects from that Category will be selected.
TESTED REVIT API: 2018
The snippet can be used as is in a Revit Application Macro for test purposes
Author: Deyan Nenov | github.com/ArchilizerLtd
This file is shared on www.revitapidocs.com
For more information visit http://github.com/gtalarico/revitapidocs
License: http://github.com/gtalarico/revitapidocs/blob/master/LICENSE.md
*/

public void FilterSelect()
{
			UIDocument uidoc = ActiveUIDocument;
			Document doc = uidoc.Document;
						
			Reference refer = uidoc.Selection.PickObject(ObjectType.Element, "Set the filter"); //Pick an object by which Category you will filter
			
			IList elements = uidoc.Selection.PickElementsByRectangle();
						
			uidoc.Selection.SetElementIds(elements
				.Where(x => x.Category.Id.IntegerValue.Equals(doc.GetElement(refer).Category.Id.IntegerValue))
				.Select(x => x.Id)
				.ToList());
}