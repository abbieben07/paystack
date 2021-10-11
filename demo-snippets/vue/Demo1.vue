<template>
	<Page>
		<ActionBar>
			<NavigationButton text="Back" android.systemIcon="ic_menu_back" @tap="$navigateBack" />
			<Label text="Demo 1" />
		</ActionBar>

		<StackLayout>
			<Label text="The version is:" />
			<Button text="Make Payment" @tap="payment" />
		</StackLayout>
	</Page>
</template>

<script>
import { Paystack } from '@abbieben/paystack';
import { knownFolders } from '@nativescript/core';
export default {
	methods: {
		payment() {
			console.log(
				knownFolders
					.currentApp()
					.getFolder('www')
					.eachEntity((e) => console.log(e.name))
			);
			const paystack = new Paystack();
			paystack.key = 'pk_test_72fab2286e4be992f1e8f1a0c71797b6cc1b7098';
			paystack.email = 'abbie_ben@live.com';
			paystack.amount = 10000 * 100;
			paystack.label = 'Demo testing';
			paystack.useBank = true;
			paystack.useQR = true;
			paystack.useUSSD = true;
			paystack.useMobileMoney = true;
			paystack.useBankTransfer = true;
			paystack
				.pay()
				.then((transaction) => console.dir(transaction))
				.catch((e) => console.error(e));
		}
	}
};
</script>

<style lang="scss" scoped></style>