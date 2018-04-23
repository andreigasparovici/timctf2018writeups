Inviation
=====

* Tools used: pdfextract, python

Firstly, we exxtracted JavaScript from the given pdf:
```sh
pdfextract --js invitation.pdf
```

The dumped JavaScript looked like this:
```js
static void create_PDFWithFormValidation() {
    PDFDocument doc = new PDFDocument(PDFOne_License.KEY);
    doc.OpenAfterCreate = true;
    doc.MeasurementUnit = PDFMeasurementUnit.Inches;

    // Create a text form field
    PDFFormTextField tf = new PDFFormTextField(new RectangleF(1f, 1f, 1f, 0.3f));
    tf.FieldName = "FullName";
    tf.BackgroundColor = Color.LightGray;
    tf.NameAsUnicode = false;

    // Create a push button form field
    PDFFormPushButton pb = new PDFFormPushButton(new RectangleF(1f, 2f, 1f, 0.3f));
    pb.FieldName = "SubmitButton";
    pb.ActionType = PDFFormFieldActionType.Javascript_Action;
    pb.NormalCaption = "Submit";
    pb.JavaScript =
	"var oNameField = this.getField('FullName'); " +
	"if (oNameField.valueAsString.length > 2) { " +
	"  var arFields = new Array('FullName'); " +
	"  this.submitForm({ " +
	"      cURL: 'http://www.gnostice.com/newsletters/demos/200804/forms_test.asp', " +
	"      aFields: arFields, " +
	"      cSubmitAs: 'HTML', " +
	"    }); " +
	"  // if validation is ok..." +
	"  // then this at the end, somehow... don't click or access, wait until I learn JS and how it works in PDF!!!!!!!!!" +
	"   var dlink = 'https://gist.github.com/0xcpu/de7c4c11b59c947bc247ae6d71c9348f';" +
	"} else { " +
	"   app.alert('Nhyet! Nhyet! Nhyet!');" +
	"}";

    // Add form fields to the document
    doc.AddFormField(tf);
    doc.AddFormField(pb);

    doc.Save("form.pdf");
    doc.Close();
}
```

It is easy to observe the variable __dlink__, which is not used throughout the script.
Following the link, we get a string which looks like a reversed base64.

We reversed it and wrote the decoded bytes to an image file:

```python
import requests
text = requests.get('https://gist.githubusercontent.com/0xcpu/de7c4c11b59c947bc247ae6d71c9348f/raw/9aa9c366ad72b04e6d072b22d77a370524de2f59/panda.txt').text
text = ''.join(text.split('\n'))
text = text[::-1]
open('image', 'w').write(text.decode('base64'))
```

The generated image had the flag:

```
timctf{h4ck_for_4_l1v1ng_pl4net}
```
