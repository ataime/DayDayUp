# naive-ui 组件使用
文档：https://www.naiveui.com/zh-CN/os-theme/components/form#API

### 在使用 naive-ui 时，会遇到这样的"n-form"属性定义.
##### 说明：
    model: 获取表项中收集到的值的对象，这个对象中的数据会和表单进行双向绑定。
    rules: 验证表项的规则
    ref: ref="formRef",这里使用 ref 属性给这个 <n-form> 组件实例设置了一个引用名 formRef。在 Vue 组件的 JavaScript 代码中，你可以通过 this.$refs.formRef（选项 API）或 refs.formRef（组合式 API）来访问这个表单实例。
    label-placement: 'top'	标签显示的位置
    label-width:	number | string | 'auto'
##### 示例：
```
    <n-form
      :model="formParams"
      :rules="rules"
      ref="formRef"
      label-placement="left"
      :label-width="80"
      class="py-4"
    >
      <n-form-item label="用户名" path="name">
        <n-input placeholder="请输入用户名" v-model:value="formParams.name" />
      </n-form-item>
      <n-form-item label="地址" path="address">
        <n-input type="textarea" placeholder="请输入地址" v-model:value="formParams.address" />
      </n-form-item>

      <n-form-item label="日期" path="date">
        <n-date-picker
          type="datetime"
          placeholder="请选择日期"
          v-model:value="formParams.date"
        />
      </n-form-item>
    </n-form>

```

