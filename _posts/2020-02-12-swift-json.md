---
layout: post
title: JSON - What's Under the Mask?
permalink: /wiki/swift-json
tag: programming
---

## JSON - What's Under the Mask?

Converting a JSON to String values is fairly straight forward.  Leveraging the built-in NSJSONSerialization object and the provided CodePug.com helper method below, String content can easily be retrieved for populating objects.

### Swift 2 - JSON Helper Method
```
        let JSONData = jsonStringContent.dataUsingEncoding(NSUTF8StringEncoding)
        do {
            let json = try NSJSONSerialization.JSONObjectWithData(JSONData!, options: .AllowFragments) as! [String: AnyObject]
            print(valueForKeyPath(json, key: "description.text"))
        } catch {
            print("error serializing JSON: \(error)")
        }

    func valueForKeyPath(json:[String:AnyObject], key:String) -> String {
        let keys = key.componentsSeparatedByString(".")
        var parent = [String:AnyObject]()
        for k in keys {
            if k == keys.last {
                if let text = parent[k] as? String {
                    return text
                } else if let number = parent[k] as? NSNumber {
                    return "\(number)"
                }
            } else {
                if let node = json[k] as? [String:AnyObject] {
                    parent = node
                }
            }
        }
        return ""
    }
```