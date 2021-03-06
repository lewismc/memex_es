# memex_es
A number of Nutch plugins and README for persisting Nutch crawl data into a target index in a particular schema format

# Applying
```
$ svn co http://svn.apache.org/repos/asf/nutch/trunk/ nutch_trunk
$ cp memex_cdr_plugin_segments.patch nutch_trunk 
$ cd nutch_trunk
$ patch -p0 -i memex_cdr_plugin_segments.patch
```
At this stage you need to open the following file
```
$ vim conf/nutch-default.xml
```
Make sure that you populate the following configuration properties
```
<!-- Memex CDR Properties -->
<property>
  <name>memex.cdr.cluster</name>
  <value></value>
  <description>
  </description>
</property>

<property>
  <name>memex.cdr.username</name>
  <value></value>
  <description>
  </description>
</property>

<property>
  <name>memex.cdr.password</name>
  <value></value>
  <description>
  </description>
</property>

<property>
  <name>memex.cdr.index</name>
  <value></value>
  <description>
  </description>
</property>

<property>
  <name>memex.cdr.type</name>
  <value></value>
  <description>
  </description>
</property>
``` 
After that you can safely build Nutch source
```
$ ant runtime
$ cd runtime/local
```
At this stage you are ready to configure your Nutch crawler... mostly within conf/nutch-site.xml
Make sure to register the plugins within the plugin.includes property

```
 <property>
   <name>plugin.includes</name>   
   <value>protocol-http|urlfilter-regex|parse-(html|tika)|index-memex|indexer-memex|scoring-opic|urlnormalizer-(pass|regex|basic)</value>
   <description>Regular expression naming plugin directory names to
   include.  Any plugin not matching this expression is excluded.
   In any case you need at least include the nutch-extensionpoints plugin. By
   default Nutch includes crawling just HTML and plain text via HTTP,
   and basic indexing and search plugins. In order to use HTTPS please enable
   protocol-httpclient, but be aware of possible intermittent problems with the
   underlying commons-httpclient library.
   </description>
 </property>
```

If you run into any problems please email lewis [dot] j [dot] mcgibbney [at] jpl [dot] nasa [dot] gov CC'ing memex-jpl [at] googlegroups [dot] com
