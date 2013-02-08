
                       WebWork Sample Plugin for JIRA


Matt Doar, mdoar@pobox.com
Consulting Toolsmiths


Summary and Usage
=================

This plugin contains working samples to demonstrate how JIRA web pages
are generated. It assumes some basic familiarity with HTML and Java.

The plugin assumes that you have the source code to the plugin available.

To install
----------

0. Use a development instance of JIRA. Nothing will be changed
   permanently by this plugin but production servers aren't the place to
   learn new things!

   JIRA_TOP is the top-level directory of your JIRA installation

   JIRA_DATA is the JIRA home directory as defined in
   $JIRA_TOP/atlassian-jira/WEB-INF/classes/jira-application.properties

1. Check out the source code for the plugin from Subversion with

   git clone ssh://git@bitbucket.org/mdoar/webwork-sample.git

2. Build the plugin 

   cd WSMPL
   mvn package

3. Deploy the plugin jar file

   cp target/webwork-sample-4.0.jar $JIRA_DATA/plugins/installed-plugins

4. Create a new directory in your JIRA installation

   mkdir -p $JIRA_TOP/atlassian-jira/secure/custom/com/consultingtoolsmiths/jira/samples/webwork

   and copy the updatededitannouncement.jsp file to the new
   directory. This is an additional jsp file that will not affect any
   other jsp files in JIRA.

   cp src/main/resources/secure/custom/com/consultingtoolsmiths/jira/samples/webwork/updatededitannouncement.jsp $JIRA_TOP/atlassian-jira/secure/custom/com/consultingtoolsmiths/jira/samples/webwork

4. Add the following lines to the end of $JIRA_TOP/atlassian-jira/WEB-INF/classes/log4j.properties

log4j.category.com.consultingtoolsmiths.jira.samples.webwork.ActionAlpha = DEBUG, console, filelog
log4j.additivity.com.consultingtoolsmiths.jira.samples.webwork.ActionAlpha = false
log4j.category.com.consultingtoolsmiths.jira.samples.webwork.ActionBeta = DEBUG, console, filelog
log4j.additivity.com.consultingtoolsmiths.jira.samples.webwork.ActionBeta = false
log4j.logger.com.atlassian.jira.web.action.custom.EditAnnouncementBanner = DEBUG, console, filelog
log4j.additivity.com.atlassian.jira.web.action.custom.EditAnnouncementBanner = false

Without these log settings you won't see anything in the
atlassian-jira.log file when you run the samples.

5. Restart JIRA

You can also use the usual Atlassian PDK commands such as "atlas-run",
but the jsp file deploymentand logging configuration will still need
to be done manually.

To uninstall
------------

1. Remove webwork-sample-4.0.jar from $JIRA_DATA/plugins/installed-plugins

2. Remove the jsp file and the directory (optional) 

   rm -rf $JIRA_TOP/atlassian-jira/secure/custom/com/consultingtoolsmiths/jira/samples/webwork

3. Restart JIRA

Usage
-----

1. Log into the development JIRA as a user with jira admin privileges
and go to the Admin page

2. You should see a new Samples section on the left at the top containing lots of links to example pages.

3. Read the sample source code, starting with
src/main/resources/atlassian-plugin.xml and look at the output in
atlassian-jira.log when each of the links in Samples is clicked.
More detailed descriptions of what happens for each example action can
be found here:
 https://studio.plugins.atlassian.com/wiki/display/WSMPL/Webwork+Sample+Plugin

Rebuilding the plugin
---------------------

cd WSMPL
rm -rf target
mvn -o package

and deploy the file target/webwork-sample.4.0.jar as usual. If you
change a jsp file, don't forget to deploy that too. The -o option for
mvn is for offline mode and is slightly faster once you have all the
necessary jar files downloaded.


