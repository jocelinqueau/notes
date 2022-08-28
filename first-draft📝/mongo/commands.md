collection.find({ arrayElementName: { $exists: true, $not: {$size: 0} } })
