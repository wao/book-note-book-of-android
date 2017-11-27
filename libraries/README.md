# Libraries

## Gson

Gson is very handy to use.

### Dependencies

"com.google.code.gson:gson:2.8.2"

import com.google.gson.*;

### Create a Gson object

Create a default gson object:

```java
Gson gson = new Gson();
```

Or, using `GsonBuilder` to customize gson object. By using gson builder, yu can make it serialize null, which is omitted by default. You can also set pretty output for human read.

```java
GsonBuilder gb = new GsonBuilder();

gb.registerType(....);


Gson gson = gb.create();
```

Please notice gson is thread safe, rephrased in another language, you can used in several thread simatianouly without lock.


### Write out json

```
  gson.toJson( object_or_value ); //a string is return
```

### Read json

```
  gson.fromJson( string_of_json, int.class | Yourclass.class | String[].class|  etc );
```

If you want read into a Collection<Type>, due to type information erased by java compiler, you must write in following format:

```
  gson.fromJson( str_json, new TokeyType<Collection<YourType> >(){}.getType() );
```

### Non-standard json format

Gson uses default format for internal class and type, some are not suite for your needed, you can define `Serializer`, `Deserializer` and `InstanceCreater` to achieve your goal.

For example to read an OffsetDateTime from json string
```java
class OffsetDateTimeDeserializer implements JsonDeserializer<OffsetDateTime>, JsonSerializer<OffsetDateTime> {
  public OffsetDateTime deserialize(JsonElement json, Type typeOfT, JsonDeserializationContext context)
      throws JsonParseException {
      def s = json.getAsJsonPrimitive().getAsString();
    return OffsetDateTime.parse(s);
  }

     public JsonElement serialize(OffsetDateTime dt, Type typeOfId, JsonSerializationContext context) {
     return new JsonPrimitive(dt.toString());
   }
}

GsonBuilder gb = new GsonBuilder();
gb.registerTypeAdapter(OffsetDateTime.class, new OffsetDateTimeDeserializer());

Gson gson = gb.create();

def t = gson.fromJson("\"2017-11-02T07:03:04.806Z\"", OffsetDateTime.class);
```

## java.time.*
