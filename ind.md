# MongoDB 索引

 **_id  为所有文档的默认索引，所有文档都含有该索引**


* ###创建索引
    
    ```
    db.collection.createIndex( 
        <key and index type specification>, <options> 
    )
    ```
    
    3。0 版本后 ensureIndex 被放弃，被设定为 createIndex 别名
    
    > db.collection.createIndex( { 
        < keys >,
        < options >
     } )
    
    字段 key 对应 value 可取 值 1 或 -1 ，1 表示索引默认升序排序，-1 表示索引默认降序排序
    
    **options** :
    
    * background
    
        类型：boolean, 指定返回的字段  1  返回 0 不返回 如：{"a":1,"b":0} ，当设定该 projection 时 查询结构的文档中将返回 1
        
    * unique 
    
        类型：boolean, true，创建唯一索引，该选项对哈希索引不可用
        
    * name 
    
        类型：string, 索引名称，如未指定,MongoDB串联索引字段的名称和排序顺序生成索引名称
        
    * partialFilterExpression
    
        类型：document, 部分索引，可指定仅索引特条件下的文本，其它则不索引,3.2 以后的版本才有该属性
        
    * sparse
    
        类型： boolean，true，稀疏索引，索引只引用具有指定字段的文档，3.2 之后的版本应当优先使用部分索引
        
    * expireAfterSeconds
    
        类型：int ，TTL 索引，指定一个整数值(以秒为单位)，控制MongoDB集合中文档的存活时间
        
    * storageEngine
    
        类型：document,  创建索引用户自主配置存储引擎                    
* ###索引类型
    
    * 单个字段索引
    
        索引建立在单一字段上 如：
        
            db.collection.createIndex({ name : -1 })
     
    * 复合索引
     
        多个字段联合建立索引 如：
            
            db.collection.createIndex({ userid : 1, score : -1 })    
    * Multikey
    
        multikey 索引用来索引存储在数组中的内容，如果为保存数组值的字段编制索引, MongoDB 将为数组的每个元素创建单独的索引项 如：
        
            存在文档 :
            {
                "name" : "xyz",
                addr : [
                    { "zip" : "10036" },
                    { "rar" : "30005" }
                ]   
            }
            若要为 addr 数组中的 zip 字段建立索引则应:
            db.collection.createIndex( { "addr.zip" : 1 } )
            
    **此外 MongoDB 还支持地理空间索引，文本索引，哈希索引，详情可产看MongoDB文档**
    
* ###索引属性

    * 唯一索引
        
        唯一索引拒绝索引字段的重复值，插入更新集合时，MongoDB将检查是否满足唯一条件，否则插入更新失败，创建方法如下，设置unique 为true 即可
        > db.collection.createIndex({ "user_name" : 1,{ unique : true } })
    
    * 部分索引
        
        部分索引仅索引满足条件的文档。部分索引具有较低的存储需求，降低了索引创建和维护的性能成本，如：
        
            db.restaurants.createIndex(
               { cuisine: 1, name: 1 },
               { partialFilterExpression: { rating: { $gt: 5 } } }
            )
        
         该语句创建了一个复合索引的部分索引，仅当文档中的rating 值大于等于5时，才联合索引 cuisine ，name 字段
         
    * 稀疏索引
    
        稀疏索引仅包含具有索引字段的文档的条目，3.2 之后版本优先使用部分索引，创建时将options 参数spare 设定为true 即可，如：
        
            db.addresses.createIndex(
                { "xmpp_id": 1 }, { sparse: true } 
            )
            
    * TTL索引
    
        TTL索引可控制文档在集合中的存活时间，当索引时间存活时间超过TTL设定时间时，MongoDB将自动删除过期的索引与相对应的文档        
        
                 
    
                                 