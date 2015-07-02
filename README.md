> *This module was taken from a [code snippet](https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#A_little_framework.3A_a_complete_cookies_reader.2Fwriter_with_full_unicode_support) on the MDN docs for `document.cookie`. It has been published as an npm module to facilitate use.*

# doc-cookies
A little framework: a complete cookies reader/writer with full unicode support

Sometimes, cookies being formatted strings, it can be intricate to deal with them in a natural way. The following library aims to abstract the access to <code>document.cookie</code> by defining an object (<var>docCookies</var>) that is partially consistent with a <a href="https://developer.mozilla.org/en-US/docs/Web/Guide/API/DOM/Storage#Storage"><code>Storage</code> object</a>. It offers also a full unicode support.

> *Note: For never-expire-cookies we used the arbitrarily distant date <samp>Fri, 31 Dec 9999 23:59:59 GMT</samp>. If for any reason you are afraid of such a date, use the [conventional date of end of the world](http://en.wikipedia.org/wiki/Year_2038_problem) <samp>Tue, 19 Jan 2038 03:14:07 GMT</samp> – which is the maximum number of seconds elapsed since since <samp>1 January 1970 00:00:00 UTC</samp> expressible by a [signed 32-bit integer](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Operators/Bitwise_Operators#Signed_32-bit_integers) (i.e.: <samp>01111111111111111111111111111111</samp>, which is `new Date(0x7fffffff * 1e3)`).*

### Writing a cookie

###### Syntax
``` javascript
docCookies.setItem(name, value[, end[, path[, domain[, secure]]]])
```

###### Description
Create/overwrite a cookie.

###### Parameters
<dl>
<dt><var>name</var></dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_syntax">name</a> of the cookie to create/overwrite (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a>).</dd>
<dt><var>value</var></dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_syntax">value</a> of the cookie (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a>).</dd>
<dt><var>end</var> (optional)</dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_max-age"><code>max-age</code></a> in seconds (e.g. <samp>31536e3</samp> for a year, <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Infinity"><code>Infinity</code></a> for a <code>never-expires</code> cookie), or the <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_expires"><code>expires</code></a> date in <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Date/toGMTString"><code>GMTString</code></a> format or as <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Date"><code>Date</code> object</a>; if not specified the cookie will expire at the end of session (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Number"><code>number</code></a> – finite or <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Infinity"><code>Infinity</code></a> – <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a>, <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Date"><code>Date</code> object</a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null"><code>null</code></a>).</dd>
<dt><var>path</var> (optional)</dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_path">path</a> from where the cookie will be readable. E.g., <code>"/"</code>, <code>"/mydir"</code>; if not specified, defaults to the current path of the current document location (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null"><code>null</code></a>). The path must be <em>absolute</em> (see <a href="http://www.ietf.org/rfc/rfc2965.txt">RFC 2965</a>). For more information on how to use relative paths in this argument, see <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#Using_relative_URLs_in_the_path_parameter">this paragraph.</a></dd>
<dt><var>domain</var> (optional)</dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_domain">domain</a> from where the cookie will be readable. E.g., <code>"example.com"</code>, <code>".example.com"</code> (includes all subdomains) or <code>"subdomain.example.com"</code>; if not specified, defaults to the host portion of the current document location (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null"><code>null</code></a>).</dd>
<dt><var>secure</var> (optional)</dt>
<dd>The cookie will be transmitted only over <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_secure">secure</a> protocol as https (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/Boolean"><code>boolean</code></a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null"><code>null</code></a>).</dd>
</dl>

### Getting a cookie
###### Syntax
``` javascript
docCookies.getItem(name)
```
###### Description
Read a cookie. If the cookie doesn't exist a [`null`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null) value will be returned.

###### Parameters
<dl>
<dt>name</dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_syntax">name</a> of the cookie to read (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a>).</dd>
</dl>

### Removing a cookie

###### Syntax
``` javascript
docCookies.removeItem(name[, path[, domain]])
```

###### Description
Delete a cookie.

###### Parameters
<dl>
<dt><var>name</var></dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_syntax">name</a> of the cookie to remove (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a>).</dd>
<dt><var>path</var> (optional)</dt>
<dd>E.g., <code>"/"</code>, <code>"/mydir"</code>; if not specified, defaults to the current path of the current document location (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null"><code>null</code></a>). The path must be <em>absolute</em> (see <a href="http://www.ietf.org/rfc/rfc2965.txt">RFC 2965</a>). For more information on how to use relative paths in this argument, see <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#Using_relative_URLs_in_the_path_parameter">this paragraph</a>.</dd>
<dt><var>domain</var> (optional)</dt>
<dd>E.g., <code>"example.com"</code>, <code>".example.com"</code> (includes all subdomains) or <code>"subdomain.example.com"</code>; if not specified, defaults to the host portion of the current document location (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a> or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null"><code>null</code></a>).
<blockquote>
<p><em>Note: To delete cookies that span over subdomains, you need to explicitate the domain attribute in <code>removeItem()</code> as well as <code>setItem()</code>.</em></p>
</blockquote>
</dd>
</dl>

### Testing a cookie

###### Syntax
``` javascript
docCookies.hasItem(name)
```

###### Description
Check whether a cookie exists in the current position.

###### Parameters
<dl>
<dt><var>name</var></dt>
<dd>The <a href="https://developer.mozilla.org/en-US/docs/Web/API/document/cookie#new-cookie_syntax">name</a> of the cookie to test (<a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Global_Objects/String"><code>string</code></a>).</dd>
</dl>

### Getting the list of all cookies
###### Syntax
``` javascript
docCookies.keys()
```

###### Description
Returns an array of all readable cookies from this location.

## Example usage:

``` javascript
docCookies.setItem("test0", "Hello world!");
docCookies.setItem("test1", "Unicode test: \u00E0\u00E8\u00EC\u00F2\u00F9", Infinity);
docCookies.setItem("test2", "Hello world!", new Date(2020, 5, 12));
docCookies.setItem("test3", "Hello world!", new Date(2027, 2, 3), "/blog");
docCookies.setItem("test4", "Hello world!", "Wed, 19 Feb 2127 01:04:55 GMT");
docCookies.setItem("test5", "Hello world!", "Fri, 20 Aug 88354 14:07:15 GMT", "/home");
docCookies.setItem("test6", "Hello world!", 150);
docCookies.setItem("test7", "Hello world!", 245, "/content");
docCookies.setItem("test8", "Hello world!", null, null, "example.com");
docCookies.setItem("test9", "Hello world!", null, null, null, true);
docCookies.setItem("test1;=", "Safe character test;=", Infinity);
 
alert(docCookies.keys().join("\n"));
alert(docCookies.getItem("test1"));
alert(docCookies.getItem("test5"));
docCookies.removeItem("test1");
docCookies.removeItem("test5", "/home");
alert(docCookies.getItem("test1"));
alert(docCookies.getItem("test5"));
alert(docCookies.getItem("unexistingCookie"));
alert(docCookies.getItem());
alert(docCookies.getItem("test1;="));
```
