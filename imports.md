<h1><a name="imports">World imports</a></h1>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#wasi:logging_logging"><code>wasi:logging/logging</code></a></li>
</ul>
</li>
</ul>
<h2><a name="wasi:logging_logging">Import interface wasi:logging/logging</a></h2>
<p>WASI Logging is a logging API intended to let users emit log messages with
simple priority levels and context values.</p>
<hr />
<h3>Types</h3>
<h4><a name="level"><code>enum level</code></a></h4>
<p>A log level, describing a kind of message.</p>
<h5>Enum Cases</h5>
<ul>
<li>
<p><a name="level.trace"><code>trace</code></a></p>
<p>Describes messages about the values of variables and the flow of
control within a program.
</li>
<li>
<p><a name="level.debug"><code>debug</code></a></p>
<p>Describes messages likely to be of interest to someone debugging a
program.
</li>
<li>
<p><a name="level.info"><code>info</code></a></p>
<p>Describes messages likely to be of interest to someone monitoring a
program.
</li>
<li>
<p><a name="level.warn"><code>warn</code></a></p>
<p>Describes messages indicating hazardous situations.
</li>
<li>
<p><a name="level.error"><code>error</code></a></p>
<p>Describes messages indicating serious errors.
</li>
<li>
<p><a name="level.critical"><code>critical</code></a></p>
<p>Describes messages indicating fatal errors.
</li>
</ul>
<hr />
<h3>Functions</h3>
<h4><a name="log"><code>log: func</code></a></h4>
<p>Emit a log message.</p>
<p>A log message has a <a href="#level"><code>level</code></a> describing what kind of message is being
sent, a context, which is an uninterpreted string meant to help
consumers group similar messages, and a string containing the message
text.</p>
<h5>Params</h5>
<ul>
<li><a name="log.level"><a href="#level"><code>level</code></a></a>: <a href="#level"><a href="#level"><code>level</code></a></a></li>
<li><a name="log.context"><code>context</code></a>: <code>string</code></li>
<li><a name="log.message"><code>message</code></a>: <code>string</code></li>
</ul>
