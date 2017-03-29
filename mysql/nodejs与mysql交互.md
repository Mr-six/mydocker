## nodejs与mysql 交互
在执行数据操作时，使用连接池来管理连接

    const mysql      = require('mysql')

    pool = mysql.createPool({
      host     : 'localhost',
      user     : 'wechat',
      password : 'html',
      database:  'wechat'
    })


    function saveInfo (info) {
      // 连接
      pool.getConnection(function(err, connection) {
        if (err) {
          console.error('error connecting: ' + err.stack)
          return
        }
        console.log('connected as id ' + connection.threadId)
        // 写入数据
        var userAddSql = 'INSERT INTO nibansh(id,prov,tel,time) VALUE(0,?,?,?)'
        var userAddSql_parse = [info.province,info.tel,info.time]
        connection.query(userAddSql,userAddSql_parse,
          function(err, rows) {
            if (err) {
              console.error('error connecting: ' + err.stack)
              // 关闭数据库连接
              connection.end()
              return
            } else {
              // console.log(rows)
              console.log('一条数据写入成功')
              connection.release()
            }
        })
      });
    }


    // 获取数据
    function getInfo () {
      return new Promise((resolve, reject) => {
        pool.getConnection(function(err, connection) {
          if (err) {
            console.error('error connecting: ' + err.stack)
            reject(err)
          }
          // 使用连接
          connection.query( 'SELECT * FROM nibansh', function(err, results, fields) {
            if (err) {
              console.error('error connecting: ' + err.stack)
              connection.release();
              return 
            }
            resolve(results)
            // 释放连接
            connection.release()
          })
        })
      })
    }

    var db_sql = {
      saveInfo: saveInfo,
      getInfo: getInfo
    }
    module.exports = db_sql
