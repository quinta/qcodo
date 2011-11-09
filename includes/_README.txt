This is the central location for all include files.  Feel free to include
any new classes or include files in this directory.


**** configuration.inc.php ****

This contains server-level configuration information (e.g. database connection
information, docroot paths (including subfoldering and virtual directories),
etc.  You must make modifications to this file to have it reflect the
configuration of your system.

See the inline documentation in qcodo/_core/configuration.inc.php-full for 
more information.


**** prepend.inc.php ****

This is the top-level include file for any and all PHP scripts which use
Qcodo.  This file checks basic location configuration and require()s the
QApplication class file (see next entry) to initialize the framework.

See the inline documentation in prepend.inc.php for more information.


**** QApplication.class.php ****

Global, application-wide loaders, settings, etc. are in this file. You must copy
the distribution example QApplication.class.php-dist to QApplication.class.php
when installing QCodo, this will be your main "Application" class file for the 
framework.

Feel free to make modifications/changes/additions to this file as you wish.
Note that the QApplication class is defined in prepend.inc as well.  Feel free
to make changes, override methods, or add functionality to QApplication as
needed. 

See the inline documentation in QApplication.class.php for more information.

**** qcodo/ ****

The qcodo/ subdirectory contains the codebase for the qcodo framework, itself.

	** CodeGen, QForm and QControl Customizations

	If you want to make *customizations* to parts of the Qcodo framework, you can
	make customizations in the following places inside of qcodo/:

	* CodeGen customizations, as well as CodeGen templates/subtemplates changes,
	  can be made in the qcodo/codegen/ subdirectory
	* QForm and any QControl customizations can be made in the qcodo/qform/ subdirectory
	* New or other downloaded QControls that are not put in core can be put into
	  the qcodo/qform/ directory

	** Qcodo Core

	The qcodo/_core/ directory contains the "core" code that is not meant to be
	modified by most end users, excpet in cases where you are adding non-standard
	functionality or making bug fixes, etc.

	If you are making changes to files in qcodo/_core/ to fix core bugs/issues/errors,
	or to add functionality in Qcodo that does not exist, you are encouraged to post
	your changes to the Qcodo Forums (http://www.qcodo.com/forums/) so that those
	changes/fixes can hopefully be integrated into the Qcodo core.


**** CODE GENERATION DIRECTORIES ****
 - data_classes/ 
 - data_classes/generated/
 - data_meta_controls/
 - data_meta_controls/generated/

These directories are created when you code generate, and contain the code
generated classes.  Note that the files in any directory named "generated"
will ALWAYS be overwritten by the code generator.

HOWEVER, the files in the top level directories ( "data_classes","data_meta_controls")
are subclasses of the ORM base classes for modification and will NEVER be overwritten.
Therefore, you should FEEL FREE to make ANY CUSTOMIZATIONS to your data 
classes IN THE DATA_CLASSES DIRECTORIES, leaving the generated base class files
in the subdirectories "generated/" alone.

You can see the "Customized Business Logic" example in Section 2 on the
Examples Site for more information.

NOTE that there are also generated files in the www/drafts and www/drafts/panels directories;
these are scaffolding - default CRUD capable UI files that you can use. Simply copy these to a
different location and alter them for your needs - BUT BEWARE! Those drafts _will_ be overwritten
on the next code generation so BE SURE YOU MOVE THEM OUT OF THE WAY TO SAVE ANY CHANGES 
you have made. The form and panel drafts and the ORM and MetaControl base classes
are all overwritten during code generation to reflect changes in the database schema.


**** MISC

If you wish to run Qcodo without any QForm interactions, simply comment out the following lines in qcodo.inc.php:

	QApplicationBase::$PreloadedClassFile['_enumerations'] = __QCODO_CORE__ . '/qform/_enumerations.inc.php';
	QApplicationBase::$PreloadedClassFile['QControlBase'] = __QCODO_CORE__ . '/qform/QControlBase.class.php';
	QApplicationBase::$PreloadedClassFile['QControl'] = __QCODO__ . '/qform/QControl.class.php';
	QApplicationBase::$PreloadedClassFile['QFormBase'] = __QCODO_CORE__ . '/qform/QFormBase.class.php';
	QApplicationBase::$PreloadedClassFile['QForm'] = __QCODO__ . '/qform/QForm.class.php';
	QApplicationBase::$PreloadedClassFile['_actions'] = __QCODO_CORE__ . '/qform/_actions.inc.php';
	QApplicationBase::$PreloadedClassFile['_events'] = __QCODO_CORE__ . '/qform/_events.inc.php';

With those lines commented out, nothing QForm-related will ever get loaded into your application.