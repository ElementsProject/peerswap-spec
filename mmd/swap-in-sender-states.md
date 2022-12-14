```mermaid
stateDiagram-v2
State_SwapInSender_BroadcastOpeningTx
State_SwapInSender_BroadcastOpeningTx --> State_SwapInSender_SendTxBroadcastedMessage: Event_ActionSucceeded
State_SwapInSender_BroadcastOpeningTx --> State_SendCancel: Event_ActionFailed
State_SwapInSender_ClaimSwapCoop
State_SwapInSender_ClaimSwapCoop --> State_ClaimedCoop: Event_ActionSucceeded
State_SwapInSender_ClaimSwapCoop --> State_WaitCsv: Event_ActionFailed
State_ClaimedCsv
[*] --> State_SwapInSender_CreateSwap: Event_SwapInSender_OnSwapInRequested
State_SwapInSender_SendRequest
State_SwapInSender_SendRequest --> State_SwapInSender_AwaitAgreement: Event_ActionSucceeded
State_SwapInSender_SendRequest --> State_SwapCanceled: Event_ActionFailed
State_SwapInSender_AwaitClaimPayment
State_SwapInSender_AwaitClaimPayment --> State_WaitCsv: Event_OnCancelReceived
State_SwapInSender_AwaitClaimPayment --> State_SwapInSender_ClaimSwapCoop: Event_OnCoopCloseReceived
State_SwapInSender_AwaitClaimPayment --> State_WaitCsv: Event_Invalid_Message
State_SwapInSender_AwaitClaimPayment --> State_ClaimedPreimage: Event_OnClaimInvoicePaid
State_SwapInSender_AwaitClaimPayment --> State_SwapInSender_ClaimSwapCsv: Event_OnCsvPassed
State_WaitCsv
State_WaitCsv --> State_SwapInSender_ClaimSwapCsv: Event_OnCsvPassed
State_WaitCsv --> State_SwapInSender_ClaimSwapCoop: Event_OnCoopCloseReceived
State_SwapCanceled
State_ClaimedPreimage
State_ClaimedCoop
State_SwapInSender_CreateSwap
State_SwapInSender_CreateSwap --> State_SwapInSender_SendRequest: Event_ActionSucceeded
State_SwapInSender_CreateSwap --> State_SwapCanceled: Event_ActionFailed
State_SendCancel
State_SendCancel --> State_SwapCanceled: Event_ActionSucceeded
State_SendCancel --> State_SwapCanceled: Event_ActionFailed
State_SwapInSender_ClaimSwapCsv
State_SwapInSender_ClaimSwapCsv --> State_ClaimedCsv: Event_ActionSucceeded
State_SwapInSender_ClaimSwapCsv --> State_SwapInSender_ClaimSwapCsv: Event_OnRetry
State_SwapInSender_AwaitAgreement
State_SwapInSender_AwaitAgreement --> State_SwapCanceled: Event_OnCancelReceived
State_SwapInSender_AwaitAgreement --> State_SendCancel: Event_OnTimeout
State_SwapInSender_AwaitAgreement --> State_SwapInSender_BroadcastOpeningTx: Event_SwapInSender_OnAgreementReceived
State_SwapInSender_AwaitAgreement --> State_SendCancel: Event_Invalid_Message
State_SwapInSender_SendTxBroadcastedMessage
State_SwapInSender_SendTxBroadcastedMessage --> State_SwapInSender_AwaitClaimPayment: Event_ActionSucceeded
State_SwapInSender_SendTxBroadcastedMessage --> State_WaitCsv: Event_ActionFailed
```