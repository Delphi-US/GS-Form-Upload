function doGet(e) {
  var doc = SpreadsheetApp.openById('SPREADSHEET_ID');
  doc.setActiveSheet(doc.getSheets()[0]);
  
  var app = UiApp.createApplication().setTitle('W2 Start');
  var panel = app.createVerticalPanel();
  var form = app.createFormPanel();
  var grid = app.createGrid(10,4).setId('startGrid');
  
  var firstName = app.createTextBox().setWidth('150px').setName('fn').setId('fn');
  var lastName = app.createTextBox().setWidth('150px').setName('ln').setId('ln');
  var email = app.createTextBox().setWidth('150px').setName('email').setId('email');
  var address = app.createTextBox().setWidth('150px').setHeight('50px').setName('address').setId('address');
  var phone = app.createTextBox().setWidth('150px').setName('phone');

  var appDatebox = app.createDateBox().setWidth('150px').setName('date');
  
  var maritalStatus = app.createListBox().setWidth('150px').setName('maritalStatus').setId('ms');
      maritalStatus.addItem('Select Option');     
      maritalStatus.addItem('Single');
      maritalStatus.addItem('Married');
  
  var dependants = app.createListBox().setWidth('50px').setName('dependants');
      dependants.addItem('#');
      dependants.addItem('0');
      dependants.addItem('1');
      dependants.addItem('2');
      dependants.addItem('3');
  var submitButton = app.createSubmitButton('<B>Submit</B>').setEnabled(false); 
  var warning = app.createHTML('Please fill in all fields').setStyleAttribute('background','#FFcc99').setStyleAttribute('fontSize','20px');
  
  //file upload
  var i9 = app.createFileUpload().setWidth('150px').setName('i9').setId('file0');
  var w4 = app.createFileUpload().setName('w4').setId('file1');
  var ec = app.createFileUpload().setName('ec').setId('file2');
  var sa = app.createFileUpload().setName('sa').setId('file3');
  var ddf = app.createFileUpload().setName('ddf').setId('file4');
  var mrs = app.createFileUpload().setName('mrs').setId('file5');
  var id = app.createFileUpload().setName('id').setId('file6');
  
  var cliHandler2 = app.createClientHandler()
  .validateLength(firstName, 1, 40).validateLength(lastName, 1, 40).validateLength(email, 1, 40).validateLength(address, 1, 40)
  .validateNotMatches(maritalStatus,'Select Option').validateNotMatches(dependants, '#').validateMatches(appDatebox, '2','g')
  //.validateNotMatches(i9, 'fileUploaded')
  .forTargets(submitButton).setEnabled(true).forTargets(warning)
  .setHTML('Now you can submit your form').setStyleAttribute('background','#99FF99').setStyleAttribute('fontSize','12px')

  //Grid layout of items on form
  grid.setText(1, 0, "First Name")
      .setWidget(1, 1, firstName.addKeyUpHandler(cliHandler2))
      .setText(1, 2, "Last Name")
      .setWidget(1, 3, lastName.addKeyUpHandler(cliHandler2))
      .setText(2, 0, "Email")
      .setWidget(2, 1, email.addKeyUpHandler(cliHandler2))
      .setText(2, 2, "Phone")
      .setWidget(2, 3, phone.addKeyUpHandler(cliHandler2))
      .setText(3, 0, 'Start Date')
      .setWidget(3, 1, appDatebox)
      .setText(4, 0, 'Marital Status')
      .setWidget(4, 1, maritalStatus.addClickHandler(cliHandler2))
      .setText(5, 0, '# of Dependants')
      .setWidget(5, 1, dependants.addClickHandler(cliHandler2))
      .setText(5, 2, 'DirectDeposit')
      .setWidget(5, 3, ddf.addChangeHandler(cliHandler2))
      .setText(6, 0, 'I9')
      .setWidget(6, 1, i9.addChangeHandler(cliHandler2))
      .setText(6, 2, 'W4')
      .setWidget(6, 3, w4.addChangeHandler(cliHandler2))
      .setText(7, 0, 'emergency contact')
      .setWidget(7, 1, ec.addChangeHandler(cliHandler2))
      .setText(7, 2, 'signed agreement')
      .setWidget(7, 3, sa.addChangeHandler(cliHandler2))
      .setText(8, 0, 'manager reference sheet')
      .setWidget(8, 1, mrs.addChangeHandler(cliHandler2))
      .setText(8, 2, 'id')
      .setWidget(8, 3, id.addChangeHandler(cliHandler2))
      .setWidget(9, 0, submitButton)
      .setWidget(9, 1, warning);

  //var cliHandl app.createClientHandler().forTargets(warning).setHTML('<B>PLEASE WAIT WHILE DATA IS UPLOADING<B>').setStyleAttribute('background','yellow');
  //var submitHandler = app.createServerClickHandler('submit');
  //submitButton.addClickHandler(submitHandler).setEnabled(true);
  
  //submitHandler.addCallbackElement(grid);
  
  panel.add(grid);
  //panel.add(app.createFileUpload().setName('thefile'));
  var statusLabel = app.createLabel().setId('status').setVisible(false);
  panel.add(statusLabel);
  form.add(panel);
  app.add(form);
  
  return app;
}

// Close everything return when the close button is clicked
function close() {
  var app = UiApp.getActiveApplication();
  app.close();
  // The following line is REQUIRED for the widget to actually close.
  return app;
}

// function called when submit button is clicked
function doPost(e) {

  // Write the data in the text boxes back to the Spreadsheet
  var doc = SpreadsheetApp.openById('SPREADSHEET_ID');
  doc.setActiveSheet(doc.getSheets()[0]);
  
  var lastRow = doc.getLastRow();
  var cell = doc.getRange('a1').offset(lastRow, 0);
  cell.setValue(e.parameter.fn);
  cell.offset(0, 1).setValue(e.parameter.ln);
  cell.offset(0, 2).setValue(e.parameter.email);
  cell.offset(0, 3).setValue(e.parameter.address);
  cell.offset(0, 4).setValue(e.parameter.date);
  cell.offset(0, 5).setValue(e.parameter.maritalStatus);
  cell.offset(0, 6).setValue(e.parameter.dependants);
 
  
  var dropbox = e.parameter.fn + " " + e.parameter.ln;
  var folder, folders = DriveApp.getFoldersByName(dropbox);
  var cf = DriveApp.getFolderById("FOLDER_ID");
    
    if (folders.hasNext()) {
      folder = folders.next();
    } else {
      folder = DriveApp.createFolder(dropbox);
      cf.addFolder(folder);
    }
 
  var app = UiApp.getActiveApplication();
  
  var i9 = e.parameter.i9;
  var w4 = e.parameter.w4;
  var ec = e.parameter.ec;
  var sa = e.parameter.sa;
  var ddf = e.parameter.ddf;
  var mrs = e.parameter.mrs;
  var id = e.parameter.id;
  
  for (var i = 0; i < 2; i++) {
    switch(i) {
      case 0: var file = folder.createFile(i9); break;
      case 1: var file = folder.createFile(w4); break;
      case 2: var file = folder.createFile(ec); break;
      case 3: var file = folder.createFile(sa); break;
      case 4: var file = folder.createFile(ddf); break;
      case 5: var file = folder.createFile(mrs); break;
      case 6: var file = folder.createFile(id); break;
    }
    cell.offset(0, 7 + i).setValue(file);
  }
    
  try {
  // Clear the values from the text boxes so that new values can be entered
  
  app.getElementById('fn').setValue('');
  app.getElementById('ln').setValue('');
  app.getElementById('email').setValue('');
  app.getElementById('address').setValue('');
  app.getElementById('ms').setValue('Select Option');
  
  
  // Make the status line visible and tell the user the possible actions
    app.getElementById('status').setVisible(true).setText('User ' + e.parameter.fn + ' entered.' +
                                                        'To add another, type in the information and click submit. To exit, click close.');
    return app;
  } catch (error) {
    return error.toString();}
}
