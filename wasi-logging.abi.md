# Types

## <a href="#level" name="level"></a> `level`: enum

  A log level, describing a kind of message.

Size: 1, Alignment: 1

### Enum Cases

- <a href="level.trace" name="level.trace"></a> [`trace`](#level.trace)

  Describes messages about the values of variables and the flow of control
  within a program.

- <a href="level.debug" name="level.debug"></a> [`debug`](#level.debug)

  Describes messages likely to be of interest to someone debugging a program.

- <a href="level.info" name="level.info"></a> [`info`](#level.info)

  Describes messages likely to be of interest to someone monitoring a program.

- <a href="level.warn" name="level.warn"></a> [`warn`](#level.warn)

  Describes messages indicating hazardous situations.

- <a href="level.error" name="level.error"></a> [`error`](#level.error)

  Describes messages indicating serious errors.

# Functions

----

#### <a href="#log" name="log"></a> `log` 

  Emit a log message.
  
  A log message has a `level` describing what kind of message is being sent,
  a context, which is an uninterpreted string meant to help consumers group
  similar messages, and a string containing the message text.
##### Params

- <a href="#log.level" name="log.level"></a> `level`: [`level`](#level)
- <a href="#log.context" name="log.context"></a> `context`: `string`
- <a href="#log.message" name="log.message"></a> `message`: `string`

