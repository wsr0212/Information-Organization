# <center>Information-Organization</center>
<br>只做了一个很微小的工作————根据身份（indentity）进行筛选。</br>
<br>主要使用`pycharm`，并且在完成后上传github，所以几乎没有commit记录</br>
<br>具体有以下一些增加：</br>
- 最simple的——改变了一下`demo.css`中的背景图片
- 增加了一个`query.html`，包含有根据身份(undergraduate、postgradute、doctoral)筛选出的信息，并以`form`的形式呈现。
  ```
    @app.route('/query',methods=['post','get'])
    def query():
        ident = request.form.get("identity")
        print(ident)
        cursor = get_cursor()  # 打开数据库
        cursor.execute("select * from tutorial.list where identity = %s", (ident))
        lists = cursor.fetchall()
        return render_template("query.html", lists=lists)
   ```
- 对`manage.html`中，加入了一个`query`的按钮，该按钮关联的表单模仿`myModal`建立。
    ```
    <button class="btn btn-primary btn-lg"
            style="width:130px;height:30px;font-size: 15px;padding: 0;margin:0 200px 10px 200px ;background-color:royalblue;border-color: royalblue"
            data-toggle="modal" data-target="#myModal3">Query
    </button>
    ------------------------------------------------------
    <div class="modal fade" id="myModal3" tabindex="-1" role="dialog" aria-labelledby="myModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-hidden="true">
                    &times;
                </button>
                <h4 class="modal-title" id="myModalLabel">
                    Doctoral
                </h4>
            </div>
            <form action="{{ url_for("query") }}" method="post">
                <div class="modal-body">

                    <p>身份：<select name="identity">

                                     <option value="Undergraduate" >Undergraduate</option>
                                    <option value="Postgraduate" >Postgraduate</option>
                                    <option value="Doctoral" >Doctoral</option>
                                </select></p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-default" data-dismiss="modal">关闭
                    </button>
                    <button type="submit" class="btn btn-primary" value="提交">提交
                    </button>
                </div>
            </form>
        </div><!-- /.modal-content -->
    </div><!-- /.modal -->
</div>

