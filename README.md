 <HTML><HEAD><TITLE>Manpage of pysa</TITLE> </HEAD><BODY> <H1>pysa</H1> Section: pysa man page (8)<BR>Updated: 31 May 2013<BR><A HREF="#index">Index</A> <A HREF="#">Return to Main Contents</A><HR>  <A NAME="lbAB">&nbsp;</A> <H2>NAME</H2>  pysa - Reverse Engineer Server Configurations <A NAME="lbAC">&nbsp;</A> <H2>SYNOPSIS</H2>  <B>pysa</B>  [ <B>-hpq</B>  ] [ <B>-m</B>  <I>module-name</I>  ] [ <B>-o</B>  <I>output-path</I>  ] [ <B>-f</B>  <I>filter-config-path</I>  ] <A NAME="lbAD">&nbsp;</A> <H2>DESCRIPTION</H2>  <B>pysa</B>  scans your system and reverse engineers its configurations for easy replication. <P> <B>pysa</B>  was born from the simple idea that today, while the &quot;cloud revolution&quot; is in progress, it is still hard to keep track of the actual configuration of our machines and easily replicate it on another machine. <P> <B>pysa</B>  is able to scan your system, looking for different resources to deploy and generates some &quot;autoconf&quot; tools script to deploy it later on another computer. <P> See <B>RESOURCES</B>  section for complete list of managed resources. <P> <B>pysa</B>  is able to generates the configuration in puppet format (see  <B><A HREF="http://docs.puppetlabs.com/man/">puppet</A>(1)</B>  man page). <A NAME="lbAE">&nbsp;</A> <H2>OPTIONS</H2>  <DL COMPACT> <DT>-h, --help<DD> Display the short help. <DT>-p, --puppet<DD> Generates <I>Puppet</I>  output. <DT>-q, --quiet<DD> Activate quiet mode and displays only error messages. By default, <B>pysa</B>  displays all log messages. <DT>-m module-name, --module module-name<DD> Choose output module name. <P> Default value:  <B>pysa</B>  <DT>-o output-path, --output output-path<DD> Choose the output filter for generated scripts. <P> Default value:  <B>output</B>  <DT>-f filter-config-path, --filter filter-config-path<DD> Specify a filter configuration file. <P> See <B>FILTERS</B>  section for more details. </DL> <A NAME="lbAF">&nbsp;</A> <H2>RESOURCES</H2>  This section describes all the resources scanned by <B>pysa</B>  <P> By default, all item described are scanned. However, you can apply some filters to avoid or specify some. See the <B>FILTERS</B>  section. <P> At the current state, the resources objects and keys are similar to <I>Puppet</I>  types. <P> Please see <B>AUTOCONF TOOLS MODULES</B>  section to be sure to be able to handle all scanned resources. <A NAME="lbAG">&nbsp;</A> <H2>	configuration files - file</H2>  <B>pysa</B>  scans (and stores in output module) all files located in a specific location. Default <B>/etc</B>  <P> Primary key: <B>path</B>  <A NAME="lbAH">&nbsp;</A> <H2>	packages - package</H2>  <B>pysa</B>  is able to scan all packages provided by <B>yum</B>  , <B>apt-get</B>  , python <B>pip</B>  ( <B>pypi</B>  ), ruby <B>gems</B>  , nodejs packaged modules ( <B>npm</B>  ) and php packages managers ( <B>pear</B>  and <B>pecl</B>  ). <P> Furthermore, <B>pysa</B>  is able to detect repositories <B>rpm</B>  packages if <B>yum</B>  is not present. <P> Primary key: <B>name</B>  <A NAME="lbAI">&nbsp;</A> <H2>	services - service</H2>  <B>pysa</B>  detects all startup services managed by <B>upstart</B>  and <B>SysV init</B>  scripts. <P> Please see <B>NOTES</B>  section. <P> Primary key: <B>name</B>  <A NAME="lbAJ">&nbsp;</A> <H2>	hosts - host</H2>  <B>pysa</B>  scans and reproduces existing hostname associations (default  <B>/etc/hosts</B>  ). <P> Primary key: <B>name</B>  <A NAME="lbAK">&nbsp;</A> <H2>	users - user</H2>  <B>pysa</B>  scans and reproduces existing users ( <B>/etc/passwd</B>  ). <P> Primary key: <B>name</B>  <A NAME="lbAL">&nbsp;</A> <H2>	groups - group</H2>  <B>pysa</B>  scans and reproduces existing groups ( <B>/etc/groups</B>  ). <P> Primary key: <B>name</B>  <A NAME="lbAM">&nbsp;</A> <H2>	mounts - mount</H2>  <B>pysa</B>  scans and reproduces existing mount points ( <B>/etc/fstab</B>  ). <P> Primary key: <B>device</B>  <A NAME="lbAN">&nbsp;</A> <H2>	crons - cron</H2>  <B>pysa</B>  scans and reproduces user's crons. <P> Primary key: <B>name</B>  <A NAME="lbAO">&nbsp;</A> <H2>	ssh keys - key</H2>  <B>pysa</B>  scans and reproduces root SSH keys (default  <B>/root/.ssh</B>  ). The scan must be done by root to assure this feature. <P> SSH keys are manages as files. <P> Primary key: <B>name</B>  <A NAME="lbAP">&nbsp;</A> <H2>	sources repositories - source</H2>  <B>pysa</B>  is able to recognize all source repositories managed by the most common SCM ( <B>subversion</B>  , <B>git</B>  and <B>mercurial</B>  ) present in the system. <P> Primary key: <B>path</B>  <A NAME="lbAQ">&nbsp;</A> <H2>	package managers repositories - repository</H2>  <B>pysa</B>  scans and reproduces <B>yum</B>  and <B>apt-get</B>  repositories. <P> Primary key: <B>name</B>  <A NAME="lbAR">&nbsp;</A> <H2>AUTOCONF TOOLS MODULES</H2>  This section lists the autoconf tools' modules which may be used. <P> Modules are used for particular features and are only needed in some particular cases. Of course, modules (as with the autoconf tools) have to be installed on the new machine, not the original one. <A NAME="lbAS">&nbsp;</A> <H2>Puppet modules</H2>  willdurand/nodejs: add npm package manager support<BR> <P> nodes/php:  add php package manager support<BR> <P> puppetlabs/vcsrepo: add scm (sources) support<BR> <P> to install a <I>Puppet</I>  module: puppet module install *module-name* <A NAME="lbAT">&nbsp;</A> <H2>FILTERS</H2>  <B>pysa</B>  integrates a powerful filters engine, which allows you to adapt its behavior to your needs. <P> A filter file is composed of sections, keys and values. In some specific cases sections and/or keys can be split using a '.' (see below for more details). <P> A key can be tagged with '_' at the front to be considered as &quot;action&quot; key. An action key is a key representing a specific action in the section (see below). <P> If some parameters conflict then the result may be harmful, please use it carefully. Don't hesitate to report any abnormal output to us. <P> Some improvements are planned in this section. <A NAME="lbAU">&nbsp;</A> <H2>	common action keys</H2>  <DL COMPACT> <DT>_contentrefer<DD> This key acts as a pointer. All the content of the referred section will be interpreted in the section. <P> This key should be set alone, as all keys will be replaced. </DL> <A NAME="lbAV">&nbsp;</A> <H2>	addition section</H2>  <DL COMPACT> <DT>section description<DD> This section is used to add or modify some values. <P> It can sounds similar to the replace section, but works in a completely different way: <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;The&nbsp;key&nbsp;is&nbsp;based&nbsp;on&nbsp;section&nbsp;key&nbsp;instead&nbsp;of&nbsp;content&nbsp;to&nbsp;replace <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;It&nbsp;is&nbsp;replaced&nbsp;at&nbsp;the&nbsp;scanning&nbsp;step,&nbsp;while&nbsp;the&nbsp;&quot; <B>replacement</B>  &quot; section is done at the output generation step <P> Remember that &quot; <B>addition</B>  &quot; is used to add/set a concrete parameter, while &quot; <B>replace</B>  &quot; is used to replace some content. <P> The section name can be separate in multiple subsections using a dot '.', always starting by &quot; <B>addition</B>  &quot; keyword: <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&quot;addition.resource_type&quot;&nbsp;will&nbsp;replace&nbsp;values&nbsp;for&nbsp;all&nbsp;objects&nbsp;of&nbsp;resource_type <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&quot;addition.resource_type.key.value&quot;&nbsp;will&nbsp;replace&nbsp;only&nbsp;the&nbsp;values&nbsp;for&nbsp;the&nbsp;objects&nbsp;where&nbsp;the&nbsp;key/value&nbsp;match&nbsp;the&nbsp;requirement <P> The key represents the resource key. <P> The value represents the resource value. <DT>section format<DD> section_key = section_value <DT>section action keys<DD> No action key for this section. </DL> <A NAME="lbAW">&nbsp;</A> <H2>	discard section</H2>  <DL COMPACT> <DT>section description<DD> This section is used to specify which object should or shouldn't be discard. <P> The key is separated in to two sub-keys by a dot '.', which represents the object type for the first one and the attribute name for the second one. <P> The values can be seen as a list of attributes separated by a coma ','. <P> The joker '*' can be used to specify to match all characters. <DT>section format<DD> object.attribute_name = attribute1, attribute2*, ... <DT>section action keys<DD> _resources: resource names <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select&nbsp;which&nbsp;resources&nbsp;to&nbsp;be&nbsp;scanned,&nbsp;use&nbsp;it&nbsp;carefully,&nbsp;some&nbsp;resources&nbsp;might&nbsp;depend&nbsp;on&nbsp;others. </DL> <A NAME="lbAX">&nbsp;</A> <H2>	replace section</H2>  <DL COMPACT> <DT>section description<DD> This section is used to replace any kind of content. <P> The section name can be separated into multiple subsections using a dot '.', always starting by &quot; <B>replace</B>  &quot; keyword: <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&quot;replace&quot;&nbsp;will&nbsp;replace&nbsp;all&nbsp;values&nbsp;for&nbsp;all&nbsp;objects. <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&quot;replace.object&quot;&nbsp;will&nbsp;replace&nbsp;all&nbsp;values&nbsp;for&nbsp;the&nbsp;selected&nbsp;object. <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;-&nbsp;&quot;replace.object.field&quot;&nbsp;will&nbsp;replace&nbsp;only&nbsp;the&nbsp;values&nbsp;associated&nbsp;with&nbsp;the&nbsp;field&nbsp;in&nbsp;the&nbsp;selected&nbsp;object. <P> The key represents the new value. <P> The value(s) represents the target to replace. <DT>section format<DD> new_value = old_value1, old_value2, ... <DT>section action keys<DD> _replaceall: true/false <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REQUIRED <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select&nbsp;the&nbsp;filtering&nbsp;mode&nbsp;(replace&nbsp;all&nbsp;except&nbsp;-true-&nbsp;or&nbsp;replace&nbsp;none&nbsp;except&nbsp;-false-) <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;default:&nbsp;true _except: primary_keys_values </DL> <A NAME="lbAY">&nbsp;</A> <H2>	update section</H2>  <DL COMPACT> <DT>section description<DD> This section is used to specify which &quot; <B>package</B>  &quot; should be updated. This section has been created due to the lack of old packages in many repositories. <P> A list of package names is specified as values of the &quot; <B>except</B>  &quot; key, separated by a coma ','. <P> The joker '*' can be used to specify to match all characters. <DT>section format<DD> except = package1, package2*, *package3, *package4*, ... <DT>section action keys<DD> _update: true/false <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;REQUIRED <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Select&nbsp;the&nbsp;filtering&nbsp;mode&nbsp;(update&nbsp;all&nbsp;except&nbsp;-true-&nbsp;or&nbsp;update&nbsp;none&nbsp;except&nbsp;-false-) <BR>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;default:&nbsp;false </DL> <A NAME="lbAZ">&nbsp;</A> <H2>USAGE EXAMPLES</H2>  See <I>docs/examples</I>  for configuration file examples. <A NAME="lbBA">&nbsp;</A> <H2>NOTES</H2>  <B>pysa</B>  has been inspired by a software called <I>Blueprint</I>  (more information at <A HREF="http://devstructure.com/blueprint/">http://devstructure.com/blueprint/</A> ) <P> <B>pysa</B>  is currently in  and so does not (always) provide 100% functional results. This comes from the architectural choices that we've made. For example, <B>pysa</B>  does not (yet) support the addition of user's packages, simply because we can't ensure the availability of these packages on the new system. <P> Furthermore, <B>pysa</B>  depends on &quot;autoconf&quot; tools. This means that if a feature is not supported by one of these tools, <B>pysa</B>  can't provide it. For example, it is currently impossible to use upstart services on a redhat-based platform, as it is impossible to use npm package manager on Ubuntu. <P> Please don't hesitate to contact us for any kind of feedback, advice or requirement: <A HREF="mailto:pysa@madeiracloud.com">pysa@madeiracloud.com</A>. <P> If you have a question about a specific source file, you can also contact the author directly (see the <B>AUTHOR</B>  section) <A NAME="lbBB">&nbsp;</A> <H2>SEE ALSO</H2>  <B><A HREF="http://docs.puppetlabs.com/man/">puppet</A>(1)</B>  <A NAME="lbBC">&nbsp;</A> <H2>BUGS</H2>  No known bugs. <A NAME="lbBD">&nbsp;</A> <H2>AUTHOR</H2>  MADEIRACLOUD LTD. (<A HREF="http://www.madeiracloud.com">www.madeiracloud.com</A>) <P> Thibault BRONCHAIN (<A HREF="mailto:thibault@mc2.io">thibault@mc2.io</A>) <P> Ken CHEN (<A HREF="mailto:ken@mc2.io">ken@mc2.io</A>) <P> Michael CHO (<A HREF="mailto:michael@mc2.io">michael@mc2.io</A>) <P>  <HR> <A NAME="index">&nbsp;</A><H2>Index</H2> <DL> <DT><A HREF="#lbAB">NAME</A><DD> <DT><A HREF="#lbAC">SYNOPSIS</A><DD> <DT><A HREF="#lbAD">DESCRIPTION</A><DD> <DT><A HREF="#lbAE">OPTIONS</A><DD> <DT><A HREF="#lbAF">RESOURCES</A><DD> <DT><A HREF="#lbAG">	configuration files - file</A><DD> <DT><A HREF="#lbAH">	packages - package</A><DD> <DT><A HREF="#lbAI">	services - service</A><DD> <DT><A HREF="#lbAJ">	hosts - host</A><DD> <DT><A HREF="#lbAK">	users - user</A><DD> <DT><A HREF="#lbAL">	groups - group</A><DD> <DT><A HREF="#lbAM">	mounts - mount</A><DD> <DT><A HREF="#lbAN">	crons - cron</A><DD> <DT><A HREF="#lbAO">	ssh keys - key</A><DD> <DT><A HREF="#lbAP">	sources repositories - source</A><DD> <DT><A HREF="#lbAQ">	package managers repositories - repository</A><DD> <DT><A HREF="#lbAR">AUTOCONF TOOLS MODULES</A><DD> <DT><A HREF="#lbAS">Puppet modules</A><DD> <DT><A HREF="#lbAT">FILTERS</A><DD> <DT><A HREF="#lbAU">	common action keys</A><DD> <DT><A HREF="#lbAV">	addition section</A><DD> <DT><A HREF="#lbAW">	discard section</A><DD> <DT><A HREF="#lbAX">	replace section</A><DD> <DT><A HREF="#lbAY">	update section</A><DD> <DT><A HREF="#lbAZ">USAGE EXAMPLES</A><DD> <DT><A HREF="#lbBA">NOTES</A><DD> <DT><A HREF="#lbBB">SEE ALSO</A><DD> <DT><A HREF="#lbBC">BUGS</A><DD> <DT><A HREF="#lbBD">AUTHOR</A><DD> </DL> <HR> This document was created by <A HREF="#">man2html</A>, using the manual pages.<BR> Time: 11:45:48 GMT, May 31, 2013 </BODY> </HTML> 