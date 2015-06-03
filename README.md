# memex_es
A Nutch plugin and README for persisting Nutch crawl data into a target index in a particular schema format

# Applying
```
$ svn co http://svn.apache.org/repos/asf/nutch/trunk/ nutch_trunk
$ cp memex_atf_plugin.patch nutch_trunk 
$ cd nutch_trunk
$ patch -p0 -i memex_atf_plugin.patch
$ ant runtime
$ cd runtime/local
```
At this stage you are ready to configure your Nutch crawler... mostly within conf/nutch-site.xml
Make sure to register the plugin within the plugin.includes property

```
1103 <property>
1104   <name>plugin.includes</name>
1105   <value>protocol-http|urlfilter-regex|parse-(html|tika)|index-memex-atf|indexer-elastic|scoring-opic|urlnormalizer-(pass|regex|basic)</value>
1106   <description>Regular expression naming plugin directory names to
1107   include.  Any plugin not matching this expression is excluded.
1108   In any case you need at least include the nutch-extensionpoints plugin. By
1109   default Nutch includes crawling just HTML and plain text via HTTP,
1110   and basic indexing and search plugins. In order to use HTTPS please enable
1111   protocol-httpclient, but be aware of possible intermittent problems with the
1112   underlying commons-httpclient library.
1113   </description>
1114 </property>
```
Additionally, you should set up your elastic search settings as follows
```
1596 <!-- Elasticsearch properties -->
1597
1598 <property>
1599   <name>elastic.host</name>
1600   <value>localhost</value>
1601   <description>The hostname to send documents to using TransportClient. Either host
1602   and port must be defined or cluster.</description>
1603 </property>
1604
1605 <property>
1606   <name>elastic.port</name>
1607   <value>9300</value>The port to connect to using TransportClient.<description>
1608   </description>
1609 </property>
1610
1611 <property>
1612   <name>elastic.cluster</name>
1613   <value></value>
1614   <description>The cluster name to discover. Either host and potr must be defined
1615   or cluster.</description>
1616 </property>
1617
1618 <property>
1619   <name>elastic.index</name>
1620   <value>memex-domains</value>
1621   <description>Default index to send documents to.</description>
1622 </property>
1623
1624 <property>
1625   <name>elastic.max.bulk.docs</name>
1626   <value>250</value>
1627   <description>Maximum size of the bulk in number of documents.</description>
1628 </property>
1629
1630 <property>
1631   <name>elastic.max.bulk.size</name>
1632   <value>2500500</value>
1633   <description>Maximum size of the bulk in bytes.</description>
1634 </property>
```

If you run into any problems please email lewis [dot] j [dot] mcgibbney [at] jpl [dot] nasa [dot] gov CC'ing memex-jpl [at] googlegroups [dot] com
