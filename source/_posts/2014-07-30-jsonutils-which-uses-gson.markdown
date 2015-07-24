---
layout: post
title: "JsonUtils which uses Gson"
date: 2014-07-30 11:00:41 +0800
comments: true
categories: [Android, Java, OpenSource]
---
``` java 
public class JsonUtil {
    public static <T> T getListFromJson(String jsonString, TypeToken typeToken) {
        Gson gson = new Gson();
        return gson.fromJson(jsonString, typeToken.getType());
    }
    public static <T> T getTFromJson(String jsonString, Class<T> t) {
        Gson gson = new Gson();
        return gson.fromJson(jsonString, t);
    }
    public static ArrayList getArrayListMapFromJson(String jsonString) {
        JsonParser jsonParser = new JsonParser();
        Gson gson = new Gson();
        JsonElement jsonElement = jsonParser.parse(jsonString);
        Logs.d(jsonElement.isJsonArray() + "   " + jsonElement.isJsonObject());
        ArrayList<HashMap<String, Object>> arrayList = new ArrayList<HashMap<String, Object>>();
        if (jsonElement.isJsonObject()) {
            arrayList.add(gson.fromJson(jsonElement, HashMap.class));
        } else if (jsonElement.isJsonArray()) {
            arrayList = getListFromJson(jsonString, new TypeToken<ArrayList<HashMap<String, Object>>>() {
            });
        }
        return arrayList;
    }
    public static ArrayList getArrayListFromJson(String jsonString) {
        JsonParser jsonParser = new JsonParser();
        Gson gson = new Gson();
        JsonElement jsonElement = jsonParser.parse(jsonString);
        Logs.d(jsonElement.isJsonArray() + "   " + jsonElement.isJsonObject());
        ArrayList arrayList = new ArrayList();
        if (jsonElement.isJsonObject()) {
            arrayList.add(gson.fromJson(jsonElement, HashMap.class));
        } else if (jsonElement.isJsonArray()) {
            arrayList = getListFromJson(jsonString, new TypeToken<ArrayList>() {
            });
        }
        return arrayList;
    }
    public static Object getObjectListFromJson(String jsonString) {
        Gson gson = new Gson();
        Object object = gson.fromJson(jsonString, new TypeToken<List<Object>>() {
        }.getType());
        return object;
    }
    public static Object getObjectFromJson(String jsonString) {
        Gson gson = new Gson();
        Object object = gson.fromJson(jsonString, Object.class);
        return object;
    }
    public static void iteratorArrayList(ArrayList arrayList) {
        Iterator it1 = arrayList.iterator();
        while (it1.hasNext()) {
            int i = 0;
            Iterator it = ((HashMap<String, String>) it1.next()).entrySet().iterator();
            while (it.hasNext()) {
                i++;
                Map.Entry entry = (Map.Entry) it.next();
                Object key = entry.getKey();
                Object value = entry.getValue();
                Logs.d("key--" + key + "  value   " + value + "\n");
            }
        }
    }
    public static void iteratorList(List inputList) {
        Iterator it1 = inputList.iterator();
        while (it1.hasNext()) {
            int i = 0;
            Iterator it = ((HashMap<String, String>) it1.next()).entrySet().iterator();
            while (it.hasNext()) {
                i++;
                Map.Entry entry = (Map.Entry) it.next();
                Object key = entry.getKey();
                Object value = entry.getValue();
                Logs.d("key--" + key + "  value   " + value + "\n");
            }
        }
    }
}

```
