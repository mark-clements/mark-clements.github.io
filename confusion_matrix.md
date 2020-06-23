#######################################
# Cross tables : confusion matrix
#######################################

# Contingency table: 'confusion matrix': rows = actual; col = prediction
#  A noter que les factor sont ici dans le même ordre (Mauvais client, Bon ..
#  Sinon il faut revoir les calculs tp, tn etc
actual <- credit4$type_de_client
predicted <- credit4$pred.proba
cross_table <- table(predicted, actual)
print(cross_table)

##        0               1 
##   0 true negative  false neg.
##   1 false positive true pos.

tp <- cross_table[2,2] # true positive (bon client)
tn <- cross_table[1,1]  # true negative (mauvais client)
fp <- cross_table[2,1] # false positive(predicted Bon client but actual Mauvais)
fn <- cross_table[1,2]  # false negative

#  true positive rate (also known as sensitivity, and recall)
tpr <- tp / (tp + fn) 
print(tpr)

# false positive rate:  how many negative values were incorrectly predicted
fpr <- fp /(fp + tn)

# true negative rate (aka Specificity): how many negative were correctly predicted
tnr <-  tn / (tn +fp)

# false negative rate
fnr <- fn / (fn + tp)

# Accuracy: overall predicted accuracy of the model
accuracy <- round((tp + tn) / sum(tp, fp, tn, fn), 3)
print(accuracy)

# precision (of positive values)
precision <- tp / (tp + fp)
print(precision)

# f score: harmonic mean of precision and recall.  0  to 1. Higher is better.
f_score <- round((2 * precision*tpr) / (precision + tpr), 3)
print(f_score)

# with Caret package; note sensitivity and specificity are inversed.
# confusionMatrix(predicted, actual)

