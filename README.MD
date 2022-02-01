## XSL-FO Processor:

- [Apache FOP](https://xmlgraphics.apache.org/fop/)

---

<img alt="Overview of OEIS tools" src="fo-struct.svg" width="50%">

---

### Links:

- https://www.w3.org/TR/xsl/
- http://www.renderx.com/tutorial.html
- http://structuredauthoring.net/xml/readings/6_Introduction_xsl_fo.html
- https://www.data2type.de/en/xml-xslt-xslfo/xsl-fo/xsl-fo-introduction/blocks
- http://www.w3big.com/xslfo/default.html
- http://www.cafeconleche.org/books/bible3/chapters/ch16.html
- https://www.antennahouse.com/xsl-fo-samples
- https://www.iro.umontreal.ca/~lapalme/ForestInsteadOfTheTrees/HTML/ch05s04.html
- https://www.netjstech.com/2015/07/how-to-create-pdf-from-xml-using-apache-fop.html
- http://www.herongyang.com/XSL-FO/
- https://docstore.mik.ua/orelly/xml/xmlnut/ch13_01.htm
- https://docs.oracle.com/cd/B40078_02/doc/bi.1013/b40017/T114602T418798.htm
- https://www.xmlpdf.com/different-first-page.html
- http://www.xmlpdf.com/builds/ibex.pdf
- https://www.data2type.de/en/xml-xslt-xslfo/xsl-fo/xsl-fo-introduction/page-layout

---

```
<?xml version="1.1" encoding="utf-8"?>
<fo:root xmlns:fo="http://www.w3.org/1999/XSL/Format1">
    <fo:layout-master-set>
        <fo:simple-page-master master-name="my_page" margin="1in">
            <fo:region-body />
        </fo:simple-page-master>
    </fo:layout-master-set>
    <fo:page-sequence master-reference="my_page">
        <fo:flow flow-name="xsl-region-body">
            <fo:block color="red" font-weight="bold" background-color="pink" padding="10pt">Hello world!</fo:block>
        </fo:flow>
    </fo:page-sequence>
</fo:root>
```

### fo:root:

The root element of all XSL-FO documents is fo:root. This element normally declares the fo prefix, which **must be** mapped to the http://www.w3.org/1999/XSL/Format namespace URI. As always, the prefix can change as long as the URI stays the same.

The fo:root element must contain two things:

- a `fo:layout-master-set` and
- a `fo:page-sequence`

### fo:layout-master-set:

Contains elements describing the overall layout of the pages themselves, that is, how large the pages are, whether they're in landscape or portrait mode, how wide the margins are.

### fo:simple-page-master:

Following are the child possible elements of the fo:simple-page-master element:

- fo:region-start
- fo:region-end
- fo:region-before
- fo:region-after
- fo:region-body

- fo:region-body is required other regions are optional.
- use extent property to set height and width of non-body element.

### fo:page-sequence:

- Page sequence is collection of pages that has same page characteristics.

- Contains the actual text that will be placed on the pages, along with the instructions for formatting.

- The formatting engine uses the layout master set to create a page. Then it adds content to the page from the fo:page-sequence until the page is full. Then it creates the next page in the sequence and places the next batch of content on that page. This process continues until all the content has been positioned.

- When formatting engine finds a page-sequence element it looks at the list of known simple-page-master and page-sequence-master elements and finds one with a master-name attribute which equals the master-reference attribute on the page-sequence.

### page-sequence:

`<fo:flow flow-name="xsl-region-body">`
`<static-content flow-name="footer">`

- flow is used add content to body.
- static-content is used to add content to header, footer or side panels.
- The order of the static-content and flow elements is important. All
  static-content elements must come before any flow elements.
- flow-name maps the region of the page where the content will be placed.
- one fo:page-sequence can not have multiple "fo:flow" declaration inside
- the content of the flow will be poured into the page body region. If the content need more space page will be added until all content of flow is exhausted.
- In order for the content contained in the flow to appear on the page, the flow-name of the flow should match a region-name of one of the regions on the page.

#### default values of flow name:

- xsl-region-body
- xsl-region-start
- xsl-region-end
- xsl-region-before
- xsl-region-after
- any custom name can be used

The fo:flow element must contain block-level formatting object elements. The most basic of these is fo:block . Others include fo:block-container , fo:list-block , fo:table , and fo:table-and-caption . We'll begin with the most basic, fo:block. A fo:block can contain a combination of raw text and formatting objects such as fo:external-graphic, fo:inline, fo:page-number, fo:footnote, and even other fo:block elements.
