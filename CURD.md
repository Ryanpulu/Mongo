# MongoDB CURD 操作

* ###find
    * 查询一条记录：db.collection.findOne()

        > db.test.findOne({"a":"b"})
    * 查询多条记录: db.collection.find()
        > db.test.find({})

    ```
    db.collection.find(
        <query>
        <projection>
    )
    ```
    查询参数说明：
    
    * query
    
        类型： document ， 查询条件
        
    * projection
    
        类型： document, 指定返回的字段  1  返回 0 不返回 如：{"a":1,"b":0} ，当设定该 projection 时 查询结构的文档中将返回 1    

* ###insert
    * 插入一条记录：db.collection.insertOne()
        > db.test.insertOne({"a":"b"})
    * 插入多条记录：db.collection.insertMany()
        > db.test.insertMany([{"a":"b"},{"c":"d"}])
    * 插入一条或多条记录：db.collection.insert()
        ```
        db.collection.insert(
           <document or array of documents>,
           {
             writeConcern: <document>,
             ordered: <boolean>
           }
        )
        ```
        **writeConcern : 写入策略**
        ```
        {w: <value>, j: <boolean> , wtimeout : <number>}
        ```
        ######W Option

        **writeConcern 说明**     

        * 1
        
            应答式写入，要求已经传播到指定的单个实例或副本集主实例（默认值）
         
        * 0
        
           非应答式写入，不返回任何响应，无法知道写入结果，相对应的式更高更快的写入速度  
           
        * majority
        
            适用于集群架构中，要求写入操作已经传递到绝大多数投票节点以及主节点进行应答
            
        * \<tag\> 
        
            要求写入操作已经传递到指定tag标记副本集中的成员后进行应答          
            
        **j Option**
        
            j : 该选项要求确认写操作已经写入journal日志之后应答客户端
                true or false
               
        **wtimeout**
        
            写入超时时间设定，单位为 ms，防止写操作无限制被阻塞
            导致无法应答客户端          

* ###update

    * 更新一条记录：db.collection.updateOne()
    ```
    db.collection.updateOne(
       <filter>,
       <update>,
       {
         upsert: <boolean>,
         writeConcern: <document>,
         collation: <document>,
         arrayFilters: [ <filterdocument1>, ... ]
       }
    )
    ```
    * 更新多条记录：db.collection.updateMany()

   ```
   db.collection.updateMany(
      <filter>,
      <update>,
      {
        upsert: <boolean>,
        writeConcern: <document>,
        collation: <document>,
        arrayFilters: [ <filterdocument1>, ... ]
      }
   )
   ```
    * 替换一条记录: db.collection.replaceOne()
    ```
    db.collection.replaceOne(
       <filter>,
       <replacement>,
       {
         upsert: <boolean>,
         writeConcern: <document>,
         collation: <document>
       }
    )
    ```

    * 更新一条或多条记录：db.collection.update()
    ```
    db.collection.update(
       <query>,
       <update>,
       {
         upsert: <boolean>,
         multi: <boolean>,
         writeConcern: <document>,
         collation: <document>,
         arrayFilters: [ <filterdocument1>, ... ]
       }
    )
    ```
    
    **update 参数说明**
    
    * query 
        
        类型：document, 更新的选择标准。可以使用与find（）方法相同的查询选择器。
     
    * update
    
        类型：document, 要应用的修改
        
    * upsert
    
        类型：boolean ，true 文档中没有则新建并插入，文档中存在则更新       
    * multi
    
        类型： boolean, true 更新多条，false 更新一条
        
    * writeConcern
    
        类型： document , 写入安全策略
            
    * arrayFilters
    
        类型： document, 筛选器 ，条件筛选，如： 
        
            [ { "x.a": { $gt: 85} }, { "x.b": { $gt: 80 } } ]   

* ###delete

    * 删除一条记录
        > db.collection.deleteOne()
    * 删除多条记录
        > db.collection.deleteMany()
    * 删除一条或多条记录
        > db.collection.remove()

    ```
    db.collection.remove(
        < query >
        < options >
    )
    ```
    ######query
        查询条件，要删除那些文档，当用 {} 表示时，将匹配所有文档

    ######options
    * justOne
      > boolean 是否仅删除一条记录，true 只删除一条文档，false 匹配文档全部删除

    * writeConcern
        > 写入安全策略
