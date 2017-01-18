<Page>
  <ActionBar title="Destinations"></ActionBar>
  <StackLayout>
    <FlexboxLayout class="container">
      <Label text="WONDERS OF ITALY" textWrap="true" class="italy"></Label>
      <Image src="https://i.imgur.com/Dx6zCYo.jpg"></Image>

      <Image src="https://i.imgur.com/UfBiMX5.jpg"></Image>
      <Label text="HIGHLIGHTS OF SOUTH AFRICA" textWrap="true" class="africa"></Label>

      <Label text="IMPERIAL CHINA" textWrap="true" class="china"></Label>
      <Image src="https://i.imgur.com/swUkmIy.jpg"></Image>
    </FlexboxLayout>
  </StackLayout>
</Page>

<Page>
  <ActionBar title="Destinations"></ActionBar>
  <StackLayout>
    <GridLayout rows="*, *, *" columns="*, *" class="container">
      <Label row="0" col="0" text="WONDERS OF ITALY" textWrap="true" class="italy"></Label>
      <Image row="0" col="1" src="https://i.imgur.com/Dx6zCYo.jpg"></Image>

      <Image row="1" col="0" src="https://i.imgur.com/UfBiMX5.jpg"></Image>
      <Label row="1" col="1" text="HIGHLIGHTS OF SOUTH AFRICA" textWrap="true" class="africa"></Label>

      <Label row="2" col="0" text="IMPERIAL CHINA" textWrap="true" class="china"></Label>
      <Image row="2" col="1" src="https://i.imgur.com/swUkmIy.jpg"></Image>
    </GridLayout>
  </StackLayout>
</Page>

.container {
  flex-wrap: wrap;
  justify-content: center;
  margin-top: 10;
}
Image, Label {
  height: 150;
  width: 150;
  border-width: 10;
}
Image {
  border-color: white;
}
Label {
  padding: 10;
  border-color: transparent;
}
.italy {
  color: white;
  background-color: #F17E47;
}
.africa {
  color: white;
  background-color: #0081A7;
}
.china {
  color: white;
  background-color: #8559B5;
}





.container {
  margin-top: 10;

}
Image, Label {
  border-width: 10;
}
Image {
  border-color: white;
}
Label {
  padding: 10;
  border-color: transparent;
}
.italy {
  color: white;
  background-color: #F17E47;
}
.africa {
  color: white;
  background-color: #0081A7;
}
.china {
  color: white;
  background-color: #8559B5;
}