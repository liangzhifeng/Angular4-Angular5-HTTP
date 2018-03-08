# Fix-the-HTTP-issue-after-upgrade-Angular4-to-Angular5

有一个新Demo从Angular4升级到Angular5，原来HTTP的请求失败。

需要修改以下地方：

# app.module.ts

将

      import { HttpModule } from '@angular/http';
      imports: [
        HttpModule
      ]
      
改为
    
     import { HttpClientModule } from '@angular/common/http';
     imports: [
          HttpClientModule,
     ],

# 组件中

     import {Http, Response} from '@angular/http';
     
    constructor(private http:Http) {
    }
     
    
    getInfo(json: any):Observable<any>{
        return this.http.get(Const.BACKEND_API_ROOT_URL + '/dashboard/clustercentre/configmng/listconfigs')
          .map((res: Response) => {
            return res.json();
          });
      }
    
    改为：
    
      import { HttpClient } from '@angular/common/http';
     
      constructor(private http: HttpClient) {
      }
      
      getInfo(){
            return this.http.get(Const.BACKEND_API_ROOT_URL + '/dashboard/clustercentre/configmng/listconfigs');
      }
    
     去掉了map, 代码更简洁。
