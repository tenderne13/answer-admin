<template>
    <div>
        <Row>
            <Col span="24">
            <Card>
                <p slot="title">
                    <Icon type="ios-list"></Icon>
                    试卷列表
                </p>
                <p slot="extra">
                    <Button type="primary" icon="plus" @click="initAdd">新增试卷</Button>
                </p>
                <Row type="flex" gutter="10" justify="center" align="middle" >
                    <Col span="24">
                        <Form ref="formInline" :model="formInline"  inline  :label-width="50">
                            <FormItem prop="user" label="名称">
                                <Input type="text"  >
                                </Input>
                            </FormItem>
                            <FormItem prop="password" label="级别">
                                <Select>
                                    <Option value="初级">初级</Option>
                                    <Option value="中级">中级</Option>
                                    <Option value="高级">高级</Option>
                                </Select>
                            </FormItem>
                            <FormItem>
                                <Button type="primary" icon="ios-search" @click="handleSubmit('formInline')">查询</Button>
                            </FormItem>
                        </Form>
                    </Col>
                </Row>
                <Row type="flex" justify="center" align="middle" class="advanced-router">
                    <Table border :columns="columns" :data="questionList" style="width: 100%;"></Table>
                </Row>
                <Page :total="10000" styles="padding-top:10px" show-total></Page>
            </Card>
            </Col>
        </Row>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                columns: [
                    {
                        title: '题目',
                        key: 'name',
                        render: (h, params) => {



                            return h('div', [
                                h('strong', params.row.name)
                            ]);
                        }
                    },
                    {
                        title: '难度',
                        key: 'level',
                        render:(h,params)=>{
                            let levelName='';
                            let level = params.row.level;
                            switch (level){
                                case 1:
                                    levelName='初级';
                                    break;
                                case 2:
                                    levelName='中级';
                                    break;
                                case 3:
                                    levelName='高级';
                                    break;
                                default:
                                    levelName='';
                            }
                            return h('div',
                                 levelName
                            );

                        }
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
	            questionList: [
                    {
                        name: '2017年最高可以获得奖',
                        level: 1,
                        address: 'New York No. 1 Lake Park'
                    },
                    {
                        name: '还他妈的遁地的',
                        level: 2,
                        address: 'London No. 1 Lake Park'
                    },
                    {
                        name: '2016年最高可以获得奖',
                        level: 3,
                        address: 'Sydney No. 1 Lake Park'
                    },
                    {
                        name: '2015年最高可以获得奖',
                        level: 2,
                        address: 'Ottawa No. 2 Lake Park'
                    },{
		                name: '2014年最高可以获得奖',
                        level: 3,
		                address: 'New York No. 1 Lake Park'
	                },
	                {
		                name: '2017年最高可以获得奖',
                        level: 1,
		                address: 'London No. 1 Lake Park'
	                },
	                {
		                name: '2017年最高可以获得奖',
                        level: 3,
		                address: 'Sydney No. 1 Lake Park'
	                },
	                {
		                name: '2017年最高可以获得奖',
                        level: 2,
		                address: 'Ottawa No. 2 Lake Park'
	                }
                ],
	            cityList: [
		            {
			            value: 'New York',
			            label: 'New York'
		            },
		            {
			            value: 'London',
			            label: 'London'
		            },
		            {
			            value: 'Sydney',
			            label: 'Sydney'
		            },
		            {
			            value: 'Ottawa',
			            label: 'Ottawa'
		            },
		            {
			            value: 'Paris',
			            label: 'Paris'
		            },
		            {
			            value: 'Canberra',
			            label: 'Canberra'
		            }
	            ]
            }
        },
        methods: {
            show (index) {
                this.$Modal.info({
                    title: 'User Info',
                    content: `Name：${this.questionList[index].name}<br>level：${this.questionList[index].level}<br>Address：${this.questionList[index].address}`
                })
            },
            remove (index) {
	            this.questionList.splice(index, 1);
            },
	        initAdd(){
		        this.$router.push({
			        name: 'questionAdd'
		        });
            }
        }
    }
</script>