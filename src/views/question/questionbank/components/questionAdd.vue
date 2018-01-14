<template>
    <div>
        <Card>
            <p slot="title">
                <Icon type="ios-list"></Icon>
                试题新增
            </p>
            <Form :model="formItem" :label-width="80">
                <FormItem label="题目">
                    <Input type="text"></Input>
                </FormItem>

                <FormItem label="难度等级">
                    <Select >
                        <Option value="初级">初级</Option>
                        <Option value="中级">中级</Option>
                        <Option value="高级">高级</Option>
                    </Select>
                </FormItem>



                <FormItem
                        v-for="(item, index) in formDynamic.items"
                        v-if="item.status"
                        :key="index"
                        :label="'选项 ' + item.index"
                        :prop="'items.' + index + '.value'"
                        :rules="{required: true, message: '选项' + item.index +' can not be empty', trigger: 'blur'}">
                    <Row>
                        <Col span="18">
                        <Input type="text" v-model="item.value" ></Input>
                        </Col>
                        <Col span="4" offset="1">
                        <Button type="ghost" @click="handleRemove(index)">删除</Button>
                        </Col>
                    </Row>
                </FormItem>

                <FormItem>
                    <Row>
                        <Col span="12">
                        <Button type="dashed" long @click="handleAdd" icon="plus-round">添加选项</Button>
                        </Col>
                    </Row>
                </FormItem>


                <!-- 选项 -->
                <FormItem label="正确选项">
                    <CheckboxGroup >
                        <Checkbox v-for="(item, index) in formDynamic.items"
                                  v-if="item.status"
                                  :key="index"
                                  :label="'选项 ' + item.index">
                        </Checkbox>
                    </CheckboxGroup>
                </FormItem>


                <FormItem>
                    <Button type="primary" @click="saveQuestion">保存</Button>
                    <Button type="ghost" style="margin-left: 8px" @click="cancleSave">取消</Button>
                </FormItem>
            </Form>
        </Card>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                columns7: [
                    {
                        title: 'Name',
                        key: 'name',
                        render: (h, params) => {
                            return h('div', [
                                h('Icon', {
                                    props: {
                                        type: 'person'
                                    }
                                }),
                                h('strong', params.row.name)
                            ]);
                        }
                    },
                    {
                        title: 'Age',
                        key: 'age'
                    },
                    {
                        title: 'Address',
                        key: 'address'
                    },
                    {
                        title: 'Action',
                        key: 'action',
                        width: 150,
                        align: 'center',
                        render: (h, params) => {
                            return h('div', [
                                h('Button', {
                                    props: {
                                        type: 'primary',
                                        size: 'small'
                                    },
                                    style: {
                                        marginRight: '5px'
                                    },
                                    on: {
                                        click: () => {
                                            this.show(params.index)
                                        }
                                    }
                                }, 'View'),
                                h('Button', {
                                    props: {
                                        type: 'error',
                                        size: 'small'
                                    },
                                    on: {
                                        click: () => {
                                            this.remove(params.index)
                                        }
                                    }
                                }, 'Delete')
                            ]);
                        }
                    }
                ],
                data6: [
                    {
                        name: 'John Brown',
                        age: 18,
                        address: 'New York No. 1 Lake Park'
                    },
                    {
                        name: 'Jim Green',
                        age: 24,
                        address: 'London No. 1 Lake Park'
                    },
                    {
                        name: 'Joe Black',
                        age: 30,
                        address: 'Sydney No. 1 Lake Park'
                    },
                    {
                        name: 'Jon Snow',
                        age: 26,
                        address: 'Ottawa No. 2 Lake Park'
                    }
                ],
                index: 1,
                formDynamic: {
                    items: [
                        {
                            value: '',
                            index: 1,
                            status: 1
                        }
                    ]
                }
            }
        },
        methods: {
            show (index) {
                this.$Modal.info({
                    title: 'User Info',
                    content: `Name：${this.data6[index].name}<br>Age：${this.data6[index].age}<br>Address：${this.data6[index].address}`
                })
            },
            remove (index) {
                this.data6.splice(index, 1);
            },
            handleSubmit (name) {
                this.$refs[name].validate((valid) => {
                    if (valid) {
                        this.$Message.success('Success!');
                    } else {
                        this.$Message.error('Fail!');
                    }
                })
            },
            handleReset (name) {
                this.$refs[name].resetFields();
            },
            handleAdd () {
                this.index++;
                this.formDynamic.items.push({
                    value: '',
                    index: this.index,
                    status: 1
                });
            },
            handleRemove (index) {
                this.formDynamic.items[index].status = 0;
            },
            saveQuestion(){
                this.$Message.success('保存成功!');
                this.$router.push({
                    name:'questionList'
                })
            },
            cancleSave(){
                this.$router.push({
                    name:'questionList'
                })
            }
        }
    }
</script>