

# VUE中$refs的基本用法

ref 有三种用法：
　　1、ref 加在普通的元素上，用this.$refs.（ref值） 获取到的是dom元素

　　2、ref 加在子组件上，用this.$refs.（ref值） 获取到的是组件实例，可以使用组件的所有方法。在使用方法的时候直接this.$refs.（ref值）.方法（） 就可以使用了。

　　3、如何利用 v-for 和 ref 获取一组数组或者dom 节点

应注意的坑：
1、如果通过v-for 遍历想加不同的ref时记得加 :号，即 :ref =某变量 ;
这点和其他属性一样，如果是固定值就不需要加 :号，如果是变量记得加 :号。（加冒号的，说明后面的是一个变量或者表达式；没加冒号的后面就是对应的字符串常量（String））

2、通过 :ref =某变量 添加ref（即加了:号） ,如果想获取该ref时需要加 [0]，如this.$refs[refsArrayItem] [0]；如果不是:ref =某变量的方式而是 ref =某字符串时则不需要加，如this.$refs[refsArrayItem]。



1、ref 需要在dom渲染完成后才会有，在使用的时候确保dom已经渲染完成。比如在生命周期 mounted(){} 钩子中调用，或者在 this.$nextTick(()=>{}) 中调用。

2、如果ref 是循环出来的，有多个重名，那么ref的值会是一个数组 ，此时要拿到单个的ref 只需要循环就可以了。

例子1:
添加ref属性
<div id="app">
    <h1 ref="h1Ele">这是H1</h1>
    <hello ref="ho"></hello>

    <button @click="getref">获取H1元素</button>
</div>
获取注册过 ref 的所有组件或元素
methods: {
        getref() {
          // 表示从 $refs对象 中, 获取 ref 属性值为: h1ele DOM元素或组件
           console.log(this.$refs.h1Ele.innerText);
           this.$refs.h1ele.style.color = 'red';// 修改html样式

          console.log(this.$refs.ho.msg);// 获取组件数据
          console.log(this.$refs.ho.test);// 获取组件的方法
        }
      }
例子2:
Vue代码：

```html
 <!-- 列表部分 -->
                <el-table @sort-change="sortChange" ref="multipleSelection" border :data="valueDryGoodTableData" style="width: 100%">
                    <el-table-column align="left" prop="title" label="标题" min-width="80%" sortable="custom">

                        <template slot-scope="scope">
                            <a target="_blank" :class="scope.row.titleClicked?'titleClicked':''" class="hoverHand bluetext" v-html="scope.row.title" @click="titleClick(scope.row.articleUrl,scope.$index)">
                            </a>
                        </template>

​                    </el-table-column>
​                    <el-table-column align="left" prop="releaseTime" label="发布日期" min-width="11%" sortable="custom"></el-table-column>
​                    <el-table-column align="center" label="操作" min-width="9%">

                        <template slot-scope="scope">
                            <span class="operatoryTools">
                                <i title="取消收藏" v-if="scope.row.isFavour" @click="favoriteOperating(scope.row.id, scope.$index)" class="hoverHand iconStyle el-icon-star-on"></i>
                                <i title="收藏" v-else @click="favoriteOperating(scope.row.id, scope.$index)" class="hoverHand iconStyle el-icon-star-off"></i>
                                <i title="分享" @click.stop="showShareOperation(scope.$index)" class="shareTarg iconfont">&#xe678;</i>
                                <div class="share" v-if="scope.row.showShare">
                                    <img class="hoverHand shareItem" title="分享到微博" @click="shareItem('sina',$event);" src="@/images/WEIBO.png">
                                    <img class="hoverHand shareItem" title="分享到微信" @click.stop="shareItem('wx',$event);" src="@/images/WEIXIN.png">
                                    <img class="hoverHand shareItem" title="分享到QQ" @click="shareItem('qq',$event);" src="@/images/QQ.png">
                                </div>
                                <div v-show="scope.row.erweimaShare" class="erweima_share"></div>
                                <div v-show="scope.row.erweimaShare1" class="erweima_share1"></div>
                            </span>
                        </template>

​                    </el-table-column>
​                </el-table>
JS代码：

//点击清空条件，调用该方法
emptyAndSearch(){//清空条件方法
			//清空树选中状态
			this.clearTreeNodeCheck(['tree']);
			//清除排序
			this.$refs.multipleSelection.clearSort();
			//设置分页参数
			this.queryParam = {
				startRow : 1,
                pageSize : 20,
                condition:{
                }
			}
			//分页查询调用
			this.confirmSearch('statistics');
			//设置清空条件为false
			this.$store.commit('valueDryGoodDatas/SET_CLEAR_ALL',false);
		}
```

例子3:
Vue代码：

 <el-form-item
                          ref="goodPicInfoFormpicUrl"
                          :label="$t('许可证证照')"
                          class="is-required"
                          prop="picUrl">
                          <el-upload
                            :show-file-list="false"
                            :http-request="uploadImg"
                            :data="certImgform"
                            action=""
                            class="avatar-uploader">
                            <img
                              v-if="queryFrom.picUrl"
                              :src="queryFrom.picUrl"
                              class="avatar">
                            <i
                              v-else
                              class="el-icon-plus avatar-uploader-icon"/>
                          </el-upload>
                          <el-button
                            type="primary"
                            plain
                            size="mini"
                            @click="viewPcPic(queryFrom.picUrl)">{{ $t('查看') }}</el-button>
                        </el-form-item>
JS代码：

      //获取元素清除验证
              this.$refs.goodPicInfoFormpicUrl.clearValidate()
一般来讲，想获取INPUT框，首先在获取DOM元素，需document.querySelector（".input1"）获取这个dom节点，然后在获取input1的值。

但是用ref绑定之后，我们就不需要在获取dom节点了，直接在上面的input上绑定input1，然后$refs里面调用就行。

然后在javascript里面这样调用：this.$refs.input1  这样就可以减少获取dom节点的消耗了
————————————————
版权声明：本文为CSDN博主「小鸡会蹦迪」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/wh710107079/java/article/details/88243638