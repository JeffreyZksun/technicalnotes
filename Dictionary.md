**Responsibilities
  * It saves the key and value pairs.
  * The derived key and value objects must work as data types. The operator ==, = must be overridden.
  * It owns all the things saved to it.**


**Pseudo code for the implementation
```
Dictionary : IDbObject
{
                void Add(String key, ObjectId value);
                void Add(String key, int value);
                void Add(String key, long value);
                void Add(String key, bool value);
                void Add(String key, time value);
                void Add(String key, String value);
               
                DictionaryItem GetItem(const String& key);
               
                String m_name;
               
                // Define two classes for the key and value. 
                // We can benefit good expansibility from the inheritance.
                typedef std::map<DictionaryKey, DictionaryValue> KeyValueMap;
                KeyValueMap m_dataMap;
}
 
/*************************************************/
class DictionaryItem  // Manipulator class to parse the value.
{
                int AsInt();
                bool AsBoolen();
                long AsLong();
                ObjectId AsObjectId();
 
                // Use the reference to avoid data copy. 
                // Maybe we do need a copy for multi-threads.
                DictionaryKey& m_key;
                DictionaryValue& m_value;
}
 
 
/*************************************************/
class DictionaryKey
{
                operator == ();
}
class StringKey: public DictionaryKey
{
                String m_key;
}
 
 
class DictionaryValue
{
                operator == ();
}
class StringValue: public DictionaryValue
{
                String m_value;
}
class ObjectIdValue: public DictionaryValue
{
                ObjectId m_objectId;
}
 
```**

