
<!-- START-INCLUDE:repo-usage.md -->


<!-- START-INCLUDE:usage/h1.standard-parser-usage.md -->

<x-tag-head>
<x-tag-meta http-equiv="X-UA-Compatible" content="IE=edge"/>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.0.0/build/highlight.min.js"/>
--></x-tag-script>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js" />
--></x-tag-script>

<x-tag-script language="JavaScript"><!--
<X-INCLUDE url="${gradleHelpersLocation}/spa_readme.js" />
--></x-tag-script>

<x-tag-style><!--
<X-INCLUDE url="https://cdn.jsdelivr.net/gh/highlightjs/cdn-release@10.0.0/build/styles/github.min.css" />
--></x-tag-style>

<x-tag-style><!--
<X-INCLUDE url="${gradleHelpersLocation}/spa_readme.css" />
--></x-tag-style>
</x-tag-head>

# Fortify SSC Parser Plugin for Debricked results - Usage

## Introduction


<!-- START-INCLUDE:p.marketing-intro.md -->

[Fortify Application Security](https://www.microfocus.com/en-us/solutions/application-security) provides your team with solutions to empower [DevSecOps](https://www.microfocus.com/en-us/cyberres/use-cases/devsecops) practices, enable [cloud transformation](https://www.microfocus.com/en-us/cyberres/use-cases/cloud-transformation), and secure your [software supply chain](https://www.microfocus.com/en-us/cyberres/use-cases/securing-the-software-supply-chain). As the sole Code Security solution with over two decades of expertise and acknowledged as a market leader by all major analysts, Fortify delivers the most adaptable, precise, and scalable AppSec platform available, supporting the breadth of tech you use and integrated into your preferred toolchain. We firmly believe that your great code [demands great security](https://www.microfocus.com/cyberres/application-security/developer-security), and with Fortify, go beyond 'check the box' security to achieve that.

<!-- END-INCLUDE:p.marketing-intro.md -->



<!-- START-INCLUDE:repo-intro.md -->

This Fortify SSC parser plugin allows for importing [CycloneDX](https://cyclonedx.org/) SBOM files generated by [Debricked](https://debricked.com/) into SSC. Two versions of this plugin are available:

* `fortify-ssc-parser-debricked-cyclonedx.jar`
	 * Parser plugin compatible with all recent SSC versions
	 * Debricked issues are displayed on the SSC Audit page only
* `fortify-ssc-22.2+-parser-debricked-cyclonedx.jar`
	 * Parser plugin compatible with SSC 22.2 and above
	 * Debricked issues are displayed on both SSC Audit page and SSC Open Source page
	 

<!-- END-INCLUDE:repo-intro.md -->


## Plugin Installation

These sections describe how to install, upgrade and uninstall the parser plugin in SSC.

### Install & Upgrade

* Obtain the plugin binary jar file; either:
     * Download from the repository release page: https://github.com/fortify/fortify-ssc-parser-debricked-cyclonedx/releases
     * Build the plugin from source: https://github.com/fortify/fortify-ssc-parser-debricked-cyclonedx/blob/main/CONTRIBUTING.md
* If you already have another version of the plugin installed, first uninstall the previously  installed version of the plugin by following the steps under [Uninstall](#uninstall) below
* In Fortify Software Security Center:
	* Navigate to Administration->Plugins->Parsers
	* Click the `NEW` button
	* Accept the warning
	* Upload the plugin jar file
	* Enable the plugin by clicking the `ENABLE` button
  
### Uninstall

* In Fortify Software Security Center:
     * Navigate to Administration->Plugins->Parsers
     * Select the parser plugin that you want to uninstall
     * Click the `DISABLE` button
     * Click the `REMOVE` button 

## Obtain results


<!-- START-INCLUDE:parser-obtain-results.md -->

### Automated import

The easiest approach for importing Debricked results into SSC is through [fcli](https://github.com/fortify-ps/fcli), using the `fcli ssc artifact import-debricked` command. This command will download the Debricked CycloneDX SBOM file using the Debricked REST API, and then upload the SBOM file to SSC for processing by this parser plugin. 

When using fcli, there is no need to manually obtain the SBOM file, preparing a proper SSC third-party results zip-file, and uploading this zip-file to SSC. With this approach, the information in the [Manual import](#manual-import) and [Upload results](#upload-results) sections can be ignored.

### Manual import

The Debricked website allows for generating a report in CycloneDX SBOM format using the following steps:

* Navigate to the repository for which you want to generate the SBOM
* Click on the 'Generate report' button on the top-right
* Select 'SBOM'
* Click the 'Generate' button
* Extract the zip-file that is sent to your registered email address to obtain the raw CycloneDX SBOM file
    * **Note**: The instructions below for uploading the SBOM file to SSC are based on the raw CycloneDX SBOM `.json` file

These steps can also be automated through the Debricked REST API, allowing the generated SBOM either being sent to an email address, or downloaded directly through the REST API.

<!-- END-INCLUDE:parser-obtain-results.md -->


## Upload results

Results can be uploaded through the SSC web interface, REST API, or SSC client utilities like FortifyClient or [fcli](https://github.com/fortify-ps/fcli). The SSC web interface, FortifyClient and most other Fortify clients require the raw results to be packaged into a zip-file; REST API and fcli allow for uploading raw results directly.

To upload results through the SSC web interface or most clients:

* Create a `scan.info` file containing a single line as follows:   
     `engineType=DEBRICKED`
* Create a zip file containing the following:
	* The scan.info file generated in the previous step
	* The raw results file as obtained from the target system (see [Obtain results](#obtain-results) section above)
* Upload the zip file generated in the previous step to SSC
	* Using any SSC client, for example FortifyClient or Maven plugin
	* Or using the SSC web interface
	* Similar to how you would upload an FPR file
	
Both SSC REST API and fcli provide options for specifying the engine type directly, and as such it is not necessary to package the raw results into a zip-file with accompanying `scan.info` file. For example, fcli allows for uploading raw scan results using a command like the following:

`fcli ssc artifact upload -f <raw-results-file> --appversion MyApp:MyVersion --engine-type DEBRICKED`

<!-- END-INCLUDE:usage/h1.standard-parser-usage.md -->


<!-- END-INCLUDE:repo-usage.md -->


---

*[This document was auto-generated from USAGE.template.md; do not edit by hand](https://github.com/fortify/shared-doc-resources/blob/main/USAGE.md)*
