```drawRect``` - called after bound already set 


### Shadow border for view
 ```       
btnCreateOffer.layer.shadowColor = UIColor.grayColor().CGColor
btnCreateOffer.layer.shadowOpacity = 1
btnCreateOffer.layer.shadowOffset = CGSizeZero
btnCreateOffer.layer.shadowRadius = 3
btnCreateOffer.layer.cornerRadius = 3
```

### NSAttributedString Text with image in front of text
```
let noRistkImage = NSTextAttachment()
 noRistkImage.image = UIImage(hhvNamed: "info_positive")
 noRistkImage.bounds = CGRect(origin: CGPointZero, size: CGSize(width: 12, height: 10))
 
 let noRiskTextImage = NSAttributedString(attachment: noRistkImage)
 
 var text = NSMutableAttributedString(attributedString: noRiskTextImage)
 
 
 var noRiskTextValue = NSAttributedString(string: " Kein Risiko: Vertrag ist 14 Tage widerrufbar!", attributes: [NSForegroundColorAttributeName : HHVColors.greenNoRiskColor])
 
 text.appendAttributedString(noRiskTextValue)
 
```
