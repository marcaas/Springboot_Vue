<template>
  <div style="height: 100%;">
    <el-container style="height: 100%; border: 1px solid #eee">

      <el-aside width="sideWidth + 'px'" style="background-color: rgb(238, 241, 246); height: 100%;">
        <el-menu :default-openeds="['1', '3']" style="min-height: 99vh; height: 100%; overflow-x: hidden;"
          background-color="#2f4156" text-color="#fff" active-text-color="#ffd04b" :collapse-transition="true"
          :collapse="isCollapse">
          <div style="height: 60px; line-height: 60px; text-align: center;">
            <img src="../assets/logo.png" alt="" style="width: 20px; position: relative; top: 5px; margin-right: 5px;">
            <b style="color: #eee;" v-show="!isCollapse">后台管理系统</b>
          </div>
          <el-submenu index="1" style="background-color: #2f4156;">
            <template slot="title">
              <i class="el-icon-message"></i>
              <span slot="title">导航一</span>
            </template>
            <el-menu-item-group style="background-color: #2f4156;">
              <template slot="title">分组一</template>
              <el-menu-item index="1-1">选项1</el-menu-item>
              <el-menu-item index="1-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="1-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="1-4">
              <template slot="title">选项4</template>
              <el-menu-item index="1-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="2">
            <template slot="title">
              <i class="el-icon-menu"></i>
              <span slot="title">导航二</span>
            </template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="2-1">选项1</el-menu-item>
              <el-menu-item index="2-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="2-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="2-4">
              <template slot="title">选项4</template>
              <el-menu-item index="2-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
          <el-submenu index="3">
            <template slot="title">
              <i class="el-icon-setting"></i>
              <span slot="title">导航三</span>
            </template>
            <el-menu-item-group>
              <template slot="title">分组一</template>
              <el-menu-item index="3-1">选项1</el-menu-item>
              <el-menu-item index="3-2">选项2</el-menu-item>
            </el-menu-item-group>
            <el-menu-item-group title="分组2">
              <el-menu-item index="3-3">选项3</el-menu-item>
            </el-menu-item-group>
            <el-submenu index="3-4">
              <template slot="title">选项4</template>
              <el-menu-item index="3-4-1">选项4-1</el-menu-item>
            </el-submenu>
          </el-submenu>
        </el-menu>
      </el-aside>

      <el-container>

        <el-header style="font-size: 12px; border-bottom: 1px solid #ccc; line-height: 60px; display: flex;">
          <div style="flex: 1; font-size: 18px;">
            <span :class="collapseBtnClass" style="cursor: pointer" @click="collapse"></span>
          </div>
          <el-dropdown style="width: 80px; cursor: pointer;">
            <span>姓名示例</span><i class="el-icon-arrow-down" style="margin-left: 5px;"></i>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item>查看</el-dropdown-item>
              <el-dropdown-item>新增</el-dropdown-item>
              <el-dropdown-item>删除</el-dropdown-item>
            </el-dropdown-menu>
          </el-dropdown>
        </el-header>

        <el-main>
          <div style="margin: 10px 0;">
            <el-input style="width: 200px;" suffix-icon="el-icon-search" placeholder="请输入名称"></el-input>
            <el-input style="width: 200px;" suffix-icon="el-icon-search" placeholder="请输入时间" class="ml-5"></el-input>
            <el-input style="width: 200px;" suffix-icon="el-icon-search" placeholder="请输入地址" class="ml-5"></el-input>
            <el-button class="ml-5" type="primary">搜索</el-button>
            <el-button type="danger" style="float: right;">删除</el-button>
            <el-button type="primary" style="float: right;">导出</el-button>
            <el-button type="primary" style="float: right;">导入</el-button>
            <el-button type="primary" style="float: right;">新增</el-button>
          </div>

          <el-table :data="tableData" border stripe>
            <el-table-column prop="date" label="日期" width="140">
            </el-table-column>
            <el-table-column prop="name" label="姓名" width="120">
            </el-table-column>
            <el-table-column prop="address" label="地址">
            </el-table-column>
            <el-table-column>
              <template slot-scope="scope">
                <el-button type="danger" style="float: right;" class="ml-5">删除</el-button>
                <el-button type="success" style="float: right;">编辑</el-button>
              </template>
            </el-table-column>
          </el-table>
          <div style="padding: 10px 0;">
            <el-pagination :current-page="currentPage4" :page-sizes="[5, 10, 15, 20]" :page-size="10"
              layout="total, sizes, prev, pager, next, jumper" :total="400">
            </el-pagination>
          </div>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  data() {
    const item = {
      date: '2023/3/6',
      name: '姓名示例',
      address: '地址示例'
    };
    return {
      tableData: Array(10).fill(item),
      collapseBtnClass: 'el-icon-s-fold',
      isCollapse: false,
      sideWidth: 200
    }
  },
  methods: {
    collapse() {// 点击收缩按钮触发
      this.isCollapse = !this.isCollapse
      if (this.isCollapse) {
        this.sideWidth = 64
      }
    }
  }
}
</script>
