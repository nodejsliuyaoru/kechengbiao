<template>
	<div>
		<el-table :data="tableData" border style="width: 100%">
			<el-table-column prop="week" label="星期/课程" width="180">
			</el-table-column>
			<el-table-column prop="one" label="第一节" width="180">
			</el-table-column>
			<el-table-column prop="two" label="第二节">
			</el-table-column>
			<el-table-column prop="three" label="第三节">
			</el-table-column>
			<el-table-column prop="four" label="第四节">
			</el-table-column>
		</el-table>
		<el-button type="text" @click="dialogFormVisible = true">修改</el-button>

		<el-dialog title="收货地址" :visible.sync="dialogFormVisible">
			<el-form :model="form">
				<el-form-item label="课程" :label-width="formLabelWidth">
					<el-input v-model="form.name" auto-complete="off"></el-input>
				</el-form-item>
				<el-form-item label="星期" :label-width="formLabelWidth">
					<el-select v-model="form.region" placeholder="请选择星期">
						<el-option label="星期一" value="星期一"></el-option>
						<el-option label="星期二" value="星期二"></el-option>
						<el-option label="星期三" value="星期三"></el-option>
						<el-option label="星期四" value="星期四"></el-option>
						<el-option label="星期五" value="星期五"></el-option>
					</el-select>
				</el-form-item>
				<el-form-item label="第几节" :label-width="formLabelWidth">
					<el-select v-model="form.first" placeholder="请选择第几节">
						<el-option label="第一节" value="one"></el-option>
						<el-option label="第二节" value="two"></el-option>
						<el-option label="第三节" value="three"></el-option>
						<el-option label="第四节" value="four"></el-option>
					</el-select>
				</el-form-item>

			</el-form>
			<div slot="footer" class="dialog-footer">
				<el-button @click="dialogFormVisible = false">取 消</el-button>
				<el-button type="primary" @click="updata">确 定</el-button>
			</div>
		</el-dialog>
	</div>
</template>
<script>
	export default {
		data() {
				return {
					tableData: [],
					dialogTableVisible: false,
					dialogFormVisible: false,
					form: {
						name: '',
						region: '',
						date1: '',
						date2: '',
						delivery: false,
						type: [],
						resource: '',
						desc: '',
						first: ''
					},
					formLabelWidth: '120px'
				}
			},
			created() {
				this.$http.post('http://localhost:3000/', this.tableData, {
					emulateJSON: true
				}).then((e) => {
					this.tableData = e.body
				})
			},
			methods: {
				updata() {
					this.dialogFormVisible = false
					this.$http.post('http://localhost:3000/updata', this.form, {
						emulateJSON: true
					}).then((e) => {
						this.$http.post('http://localhost:3000/', this.tableData, {
							emulateJSON: true
						}).then((e) => {
							this.tableData = e.body
						})
					})
				}
			}
	}
</script>