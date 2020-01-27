# pbasu-XML-JSON-Avro-Tools

# Beautify & Validation
* https://codebeautify.org
* https://codebeautify.org/jsonviewer


# JSON Path
* http://convertjson.com/json-path-list.htm


# JSON Schema validation
* https://www.jsonschemavalidator.net/
* https://json-schema-validator.herokuapp.com/


# AVRO Schema to JSON Schema conversion
* https://json-schema-validator.herokuapp.com/avro.jsp
* https://github.com/allegro/json-avro-converter

# XPATH
* https://xmltoolbox.appspot.com/xpath_generator.html
* http://qutoric.com/sketchpath/


# XML Parsing Tool
* XML Explorer (https://xmlexplorer.github.io/), read 300MB+ files

# How to lookup value of key-value pairs in XML
<FrontendStatus xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" version="1.1" serializerVersion="1.1">
  <Name>jason-P35-DS3</Name>
  <Version>v0.28-pre-3339-g9877c07</Version>
  <State>
    <String>
      <Key>currentlocation</Key><Value>playbackbox</Value>
    </String>
    <String>
      <Key>menutheme</Key><Value>mediacentermenu</Value>
    </String>
    <String>
      <Key>state</Key><Value>idle</Value>
    </String>
  </State>
  <ChapterTimes/>
  <SubtitleTracks/>
  <AudioTracks/>
</FrontendStatus>


<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="text"/>
  <xsl:template match="/">
    <xsl:value-of select="//Key[.='state']/following-sibling::Value"/>
  </xsl:template>
</xsl:stylesheet>

-------------------------------------------------------------------------------------------------------------------------------------

Input:
<Root>
  <Entities>
    <Entity EntityName="Client">
      <Data Name="ADDR_City">Anytown</Data>
      <Data Name="ADDR_State">SC</Data>
      <Data Name="ADDR_Zip">23904</Data>
    </Entity>
  </Entities>
</Root>

Output:
<Root>
  <Entities>
    <Client>
      <ADDR_City>Anytown</ADDR_City>
      <ADDR_State>SC</ADDR_State>
      <ADDR_Zip>23904</ADDR_Zip>
    </Client>
  </Entities>
</Root>

XSLT
<?xml version="1.0" encoding="utf-8"?>
<xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="xml" indent="yes"/>

  <xsl:template match="/Root">
    <Root>
      <xsl:for-each select="Entities">
        <Entities>
          <xsl:for-each select="Entity">
            <xsl:element name="{@EntityName}">
              <xsl:for-each select="Data">
                <xsl:element name="{@Name}">
                  <xsl:value-of select="./text()"/>
                </xsl:element>
              </xsl:for-each>
            </xsl:element>
          </xsl:for-each>
        </Entities>
      </xsl:for-each>
    </Root>
  </xsl:template>
</xsl:stylesheet>

