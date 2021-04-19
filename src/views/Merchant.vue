<template>
	<div id="wrapper">
		<nav class="navbar navbar-dark align-items-start sidebar sidebar-dark accordion bg-gradient-primary p-0">
			<div class="container-fluid d-flex flex-column p-0">
				<a class="navbar-brand d-flex justify-content-center align-items-center sidebar-brand m-0" href="#">
					<div class="sidebar-brand-icon rotate-n-15">
						<i class="material-icons">local_pharmacy</i>
					</div>
					<div class="sidebar-brand-text mx-3"><span>Brand</span></div>
				</a>
				<hr class="sidebar-divider my-0" />
				<ul class="nav navbar-nav text-light" id="accordionSidebar">
					<li class="nav-item">
						<router-link to="/" class="nav-link active"><i class="fas fa-table"></i><span>Merchant Report</span></router-link>
					</li>
					<li class="nav-item">
						<router-link to="/history" class="nav-link"><i class="far fa-user-circle"></i><span>Redemption Report</span></router-link>
					</li>
				</ul>
				<div class="text-center d-none d-md-inline">
					<button class="btn rounded-circle border-0" id="sidebarToggle" type="button"></button>
				</div>
			</div>
		</nav>
		<div class="d-flex flex-column" id="content-wrapper">
			<div id="content">
				<nav class="navbar navbar-light navbar-expand bg-white shadow mb-4 topbar static-top">
					<div class="container-fluid">
						<button class="btn btn-link d-md-none rounded-circle mr-3" id="sidebarToggleTop" type="button">
							<i class="fas fa-bars"></i>
						</button>
						<form class="form-inline d-none d-sm-inline-block mr-auto ml-md-3 my-2 my-md-0 mw-100 navbar-search">
							<div class="input-group">
								<input class="bg-light form-control border-0 small" type="text" placeholder="Search for ..." v-model="search" />
								<div class="input-group-append">
									<button class="btn btn-primary py-0" type="button">
										<i class="fas fa-search"></i>
									</button>
								</div>
							</div>
						</form>
						<ul class="nav navbar-nav flex-nowrap ml-auto">
							<li class="nav-item dropdown d-sm-none no-arrow">
								<a class="dropdown-toggle nav-link" data-toggle="dropdown" aria-expanded="false" href="#"><i class="fas fa-search"></i></a>
								<div class="dropdown-menu dropdown-menu-right p-3 animated--grow-in" aria-labelledby="searchDropdown">
									<form class="form-inline mr-auto navbar-search w-100">
										<div class="input-group">
											<input class="bg-light form-control border-0 small" type="text" placeholder="Search for ..." />
											<div class="input-group-append">
												<button class="btn btn-primary py-0" type="button">
													<i class="fas fa-search"></i>
												</button>
											</div>
										</div>
									</form>
								</div>
							</li>
							<div class="d-none d-sm-block topbar-divider"></div>
							<li class="nav-item dropdown no-arrow">
								<div class="nav-item dropdown no-arrow">
									<a class="dropdown-toggle nav-link" data-toggle="dropdown" aria-expanded="false" href="#"><span class="d-none d-lg-inline mr-2 text-gray-600 small">Admin</span><img class="border rounded-circle img-profile" src="assets/img/avatars/avatar5.jpeg"/></a>
									<div class="dropdown-menu shadow dropdown-menu-right animated--grow-in">
										<a v-if="items.length > 0" class="dropdown-item" href="#">
											<i class="fas fa-user fa-sm fa-fw mr-2 text-gray-400"></i>&nbsp;
											<download-excel class="btn btn-default" :data="items" :fields='{"voucher id":"voucher_id", "voucher status": "voucher_status", "voucher date": "voucher_date", "redemption date time": "redemption_date_time", "order id": "order_id", "order date": "order_date", "order status":"order_status", "product id":"product_id", "item total":"item_total", "SKU":"SKU", "merchant":"merchant", "merchant total":"merchant_total" }' worksheet="My Worksheet" name="Brawta Merchant Report.xls" style="padding: 0;color:#2e2f37;font-size: .85rem;">
												Download
											</download-excel>
										</a>
										<a v-else class="dropdown-item" href="#"><i class="fas fa-sign-out-alt fa-sm fa-fw mr-2 text-gray-400"></i>&nbsp;Download</a>
										<a class="dropdown-item" href="#"><i class="fas fa-sign-out-alt fa-sm fa-fw mr-2 text-gray-400"></i>&nbsp;Logout</a>
									</div>
								</div>
							</li>
						</ul>
					</div>
				</nav>
				<div class="container-fluid">
					<div class="card shadow">
						<div class="card-header py-3">
							<div class="row">
								<div class="col">
									<p class="text-primary m-0 font-weight-bold">Merchant Info</p>
								</div>

								<div class="col">
									<p class="text-primary m-0 font-weight-bold text-center">
										<button class="btn btn-success" data-toggle="modal" data-target="#myModal">
											Query
										</button>
									</p>
								</div>

								<div class="col">
									<p v-if="false" class="text-primary m-0 font-weight-bold" style="text-align: right">Total: ${{ total.toFixed(2) }}</p>
								</div>
							</div>
						</div>
						<div class="card-body">
							<div class="table-responsive table mt-2" id="dataTable" role="grid" aria-describedby="dataTable_info">
								<table class="table my-0" id="dataTable">
									<thead>
										<tr>
											<th v-for="col in columnNames" :key="col">{{col}}</th>
										</tr>
									</thead>
									<tbody v-if="items.length > 0">
										<tr v-for="(item, i) in items" :key="i">
											<td>{{ item.voucher_id }}</td>
											<td>{{ item.voucher_status }}</td>
											<td>{{ item.voucher_date }}</td>
											<td>{{ item.redemption_date_time }}</td>
											<td>{{ item.order_id }}</td>
											<td>{{ item.order_date }}</td>
											<td>{{ item.order_status }}</td>
											<td>{{ item.product_id }}</td>
											<td>{{ item.item_total }}</td>
											<td>{{ item.SKU }}</td>
											<td>{{ item.merchant }}</td>
											<td>{{ item.merchant_total }}</td>
										</tr>
									</tbody>
									<tbody v-else>
										<tr>
											<td>0 Items Found</td>
										</tr>
									</tbody>
								</table>
							</div>
							<div v-if="false" class="row">
								<div class="col-md-6 align-self-center">
									<p id="dataTable_info" class="dataTables_info" role="status" aria-live="polite">
										Showing 1 to 10 of 27
									</p>
								</div>
								<div class="col-md-6">
									<nav class="d-lg-flex justify-content-lg-end dataTables_paginate paging_simple_numbers">
										<ul class="pagination">
											<li class="page-item disabled">
												<a class="page-link" href="#" aria-label="Previous"><span aria-hidden="true">«</span></a>
											</li>
											<li v-for="index in parseInt(getItems().length / pageMax) || 1" :key="index" class="page-item active">
												<a class="page-link" href="#">{{ index }}</a>
											</li>
											<li class="page-item">
												<a class="page-link" href="#" aria-label="Next"><span aria-hidden="true">»</span></a>
											</li>
										</ul>
									</nav>
								</div>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<div class="modal fade" id="myModal">
			<div class="modal-dialog">
				<div class="modal-content">
					<!-- Modal Header -->
					<div class="modal-header">
						<h4 class="modal-title">Add New Item</h4>
						<button @click="closeModal" type="button" class="close" data-dismiss="modal">
							&times;
						</button>
					</div>

					<!-- Modal body -->
					<div class="modal-body">
						<form>
							<div class="form-group">
								<label for="exampleInputEmail1">Start Date</label>
								<input class="form-control" type="date" placeholder="Date" v-model="newItem.from" />
							</div>

							<div class="form-group">
								<label for="exampleInputEmail1">End Date</label>
								<input class="form-control" type="date" placeholder="Date" v-model="newItem.to" />
							</div>
						</form>
					</div>

					<!-- Modal footer -->
					<div class="modal-footer">
						<button type="button" class="btn btn-danger" v-show="!loading" data-dismiss="modal" @click="closeModal" ref="closeBtn">
							Close
						</button>
						<button v-if="!loading" type="button" class="btn btn-success" @click="addNewItem">
							Run Query
						</button>
						<button v-else class="btn btn-primary" disabled>
							<span class="spinner-border spinner-border-sm"></span>
							Loading..
						</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Autocomplete from "@trevoreyre/autocomplete-vue";
import io from "socket.io-client";

export default {
	name: "Home",
	props: {},
	components: {
		Autocomplete,
	},
	data() {
		return {
			items: [],
			total: 0,
			search: "",
			pageMax: 10,
			currentPage: 1,
			newItem: {},
			loading: false,
			baseUrl: "https://brawta-accounts.herokuapp.com",
			columnNames: ["voucher id", "voucher code", "voucher status", "voucher date", "redemption date time", "order id", "order date", "order status", "product id", "item total", "SKU", "merchant", "merchant total"]
		};
	},
	created() {
		this.socket = io(this.server);
	},
	mounted() {
		this.socket.on("init", (data) => {
		 	console.log(data)
		});
		this.socket.on("result", (data) => {
		 	console.log(data)
		});
	},
	methods: {
		getItems() {
			let companySearch = this.items.filter((x) => x.company.includes(this.search));
			let finalRes = companySearch.filter((x) => x.date.includes(date));
			return [...new Set(finalRes)];
		},
		closeModal() {
			this.$refs.closeBtn.click();
		},
		addNewItem() {
			if (!this.newItem || !this.newItem.to || !this.newItem.from) {
				alert("All fields Need to be filled!");
				return;
			}
			this.loading = true;
			let data = {};

			data.from = this.newItem.from;
			data.to = this.newItem.to;

			this.socket.emit("MerchantSearch", data);
		}
	}
};
</script>

<style scoped>
@media (min-width: 300px) {
	.col-12.col-sm-4.col-md-3.col-lg-2.col-xl-auto.d-flex.flex-column.justify-content-center {
		padding-bottom: 15px;
	}
}

a:hover {
	text-decoration: none;
}

pre {
	white-space: pre-wrap;
}

.btn {
	color: white;
}
.contact {
	width: 100vw;
	position: fixed;
	bottom: 0;
	background-color: black;
	color: white;
	left: 0;
	text-align: center;
	overflow: hidden;
}

#frame {
	width: 100%;
	height: 80vh;
}

.specialInput {
	border: 0;
	border-bottom: 1px solid;
	border-radius: 0;
}
.specialInput:focus {
	border-bottom: 3px solid blue;
	outline: none;
}
</style>
