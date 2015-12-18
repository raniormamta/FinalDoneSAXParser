# FinalDoneSAXParser

package SAXPARSER;


import java.io.File;
import java.util.ArrayList;
import java.util.List;

import javax.xml.parsers.SAXParser;
import javax.xml.parsers.SAXParserFactory;

import org.xml.sax.Attributes;
import org.xml.sax.SAXException;
import org.xml.sax.SAXParseException;
import org.xml.sax.helpers.DefaultHandler;

public class ReadingXMLFile {
	
	private String tempVal;
	private String tempValu;
	private String tempValue;
	private String tempUom;
	private List<AppBean> list = new ArrayList<AppBean>();
	public List<AppBean> getAppList() {
		return list;
	}
	AppBean app; 
	private void parseDocument(){
		SAXParserFactory factory = SAXParserFactory.newInstance();
	try {
			
			
			SAXParser saxParser = factory.newSAXParser();
			
			
			DefaultHandler handler = new DefaultHandler() {
				FooterBean footer = null;
				HeaderBean header = null;
				AppBean app = null;
/*
				@Override
				public void startDocument() throws SAXException {
					
				}

				@Override
				public void endDocument() throws SAXException {
					
				}
*/
				@Override
				public void startElement(String uri, String localName,
						String qName, Attributes attributes)
						throws SAXException {
					//reset
					tempVal = "";
					//System.out.println("Start Element"+qName);
					if(qName.equalsIgnoreCase("Footer")){
						footer = new FooterBean();
					}
					
					if (qName.equalsIgnoreCase("Header")) {
						// create a new instance of employee
						header = new HeaderBean();
						// header.setType(attributes.getValue("type"));
					}
					if (qName.equalsIgnoreCase("App")) {
						// create a new instance of employee
						tempValu = "";
						tempValue = "";
						tempUom = "";
						app = new AppBean();
						app.setId(Long.parseLong(attributes.getValue("id")));
						app.setAction(attributes.getValue("action"));
						app.setValidate(attributes.getValue("validate"));
						app.setRef(attributes.getValue("ref"));
					}
					if (qName.equalsIgnoreCase("BaseVehicle")) {
						String id = attributes.getValue("id");
						app.setBaseVehicleId(Long.parseLong(id));
					}
					if (qName.equalsIgnoreCase("EngineBase")) {
						app.setEngineBaseId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("EngineDesignation")) {
						app.setEngineDesignationId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FuelDeliverySubType")) {
						app.setFuelDeliverySubTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("Note")) {
						String id = attributes.getValue("id");
						if (id != null) {
							app.setNoteId(Long.parseLong(id));
						}
						String lang = attributes.getValue("lang");
						if (lang != null) {
							app.setNoteLang(lang);
						}
					}
					if (qName.equalsIgnoreCase("Part")) {
						app.setPartBrandAAIAId(attributes.getValue("BrandAAIAID"));
					}
					if (qName.equalsIgnoreCase("Aspiration")) {
						app.setAspirationId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("BedLength")) {
						app.setBedLengthId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("BedType")) {
						app.setBedTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("BodyNumDoors")) {
						app.setBodyNumDoorsId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("BodyType")) {
						app.setBodyTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("BrakeABS")) {
						app.setBrakeABSId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("BrakeSystem")) {
						app.setBrakeSystemId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("CylinderHeadType")) {
						app.setCylinderHeadTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("DriveType")) {
						app.setDriveTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("EngineMfr")) {
						app.setEngineMfrId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("EngineVersion")) {
						app.setEngineVersionId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("EngineVIN")) {
						app.setEngineVINId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FrontBrakeType")) {
						app.setFrontBrakeTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FrontSpringType")) {
						app.setFrontSpringTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FuelDeliverySubType")) {
						app.setFuelDeliverySubTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FuelDeliveryType")) {
						app.setFuelDeliveryTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FuelSystemControlType")) {
						app.setFuelSystemControlTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FuelSystemDesign")) {
						app.setFuelSystemDesignId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("FuelType")) {
						app.setFuelTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("IgnitionSystemType")) {
						app.setIgnitionSystemTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("Make")) {
						app.setMakeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("MfrBodyCode")) {
						app.setMfrBodyCodeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("Model")) {
						app.setModelId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("PowerOutput")) {
						app.setPowerOutputId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("RearBrakeType")) {
						app.setRearBrakeTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("RearSpringType")) {
						app.setRearSpringTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("Region")) {
						app.setRegionId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("SteeringType")) {
						app.setSteeringTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("SteeringSystem")) {
						app.setSteeringSystemId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("SubModel")) {
						app.setSubModelId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("TransElecControlled")) {
						app.setTransElecContolledId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("TransmissionMfr")) {
						app.setTransmissionMfrId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("TransmissionMfrCode")) {
						app.setTransmissionMfrCodeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("TransmissionBase")) {
						app.setTransmissionBaseId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("TransmissionControlType")) {
						app.setTransmissionControlTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("TransmissionNumSpeeds")) {
						app.setTransmissionNumSpeedsId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("TransmissionType")) {
						app.setTransmissionTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("ValvesPerEngine")) {
						app.setValvesPerEngineId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("VehicleType")) {
						app.setVehicleTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("WheelBase")) {
						app.setWheelBaseId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("Years")) {
						app.setYearsFrom(attributes.getValue("from"));
						app.setYearsTo(attributes.getValue("to"));
					}
					if (qName.equalsIgnoreCase("PartType")) {
						app.setPartTypeId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("Qual")) {
						app.setQualId(Long.parseLong(attributes.getValue("id")));
					}
					if (qName.equalsIgnoreCase("Param")) {
							String value = attributes.getValue("value");
							if (value != null) {
								app.setqParamValue(value + "" + tempValue);
								tempValue = tempValue + ", " + value;
							}
					
							String uom = attributes.getValue("uom");
							if (uom != null) {
								app.setqParamUom(uom + "" + tempUom);
								tempUom = tempUom + ", " + uom;
							}
							
							String altvalue = attributes.getValue("altvalue");
							if (altvalue != null) {
								app.setqParamAltValue(altvalue);
							}
							String altuom = attributes.getValue("altuom");
							if (altuom != null) {
								app.setqParamAltUom(altuom);
							}
					}
					 if (qName.equalsIgnoreCase("Position")) {
						app.setPosition(tempVal);
						app.setPositionId(Long.parseLong(attributes.getValue("id")));
					}
					 if (qName.equalsIgnoreCase("Asset")) {
							String action=attributes.getValue("action");
							
							app.setAssetAction(action);
							String id=attributes.getValue("id");
							app.setAssetId(Long.parseLong(id));
							
							String ref=attributes.getValue("ref");  // =====  
							if(ref!=null && !ref.equalsIgnoreCase("")){
							app.setAssetRef(ref);}
							
							String validate=attributes.getValue("validate");
							app.setAssetValidate(validate);
							
							
						}
				}

				@Override
				public void endElement(String uri, String localName,
						String qName) throws SAXException {
					if(qName.equalsIgnoreCase("Footer")){
						new DBDao().saveFooterRecord(footer);
					} else if(qName.equalsIgnoreCase("RecordCount")){
						footer.setRecordCount(Long.parseLong(tempVal));	
					}
					
					if (qName.equalsIgnoreCase("Header")) {
						new DBDao().saveHeaderRecord(header);
					} else if (qName.equalsIgnoreCase("Company")) {
						header.setCompany(tempVal);
					} else if (qName.equalsIgnoreCase("SenderName")) {
						header.setSenderName(tempVal);
					} else if (qName.equalsIgnoreCase("SenderPhone")) {
						header.setSenderPhone(tempVal);
					} else if (qName.equalsIgnoreCase("TransferDate")) {
						header.setTransferDate(tempVal);
					} else if (qName.equalsIgnoreCase("BrandAAIAID")) {
						header.setBrandAAIAID(tempVal);
					} else if (qName.equalsIgnoreCase("DocumentTitle")) {
						header.setDocumentTitle(tempVal);
					} else if (qName.equalsIgnoreCase("EffectiveDate")) {
						header.setEffectiveDate(tempVal);
					} else if (qName.equalsIgnoreCase("SubmissionType")) {
						header.setSubmissionType(tempVal);
					} else if (qName.equalsIgnoreCase("MapperCompany")) {
						header.setMapperCompany(tempVal);
					} else if (qName.equalsIgnoreCase("MapperContact")) {
						header.setMapperContact(tempVal);
					} else if (qName.equalsIgnoreCase("MapperPhone")) {
						header.setMapperPhone(tempVal);
					} else if (qName.equalsIgnoreCase("MapperEmail")) {
						header.setMapperEmail(tempVal);
					} else if (qName.equalsIgnoreCase("VcdbVersionDate")) {
						header.setVcdbVersionDate(tempVal);
					} else if (qName.equalsIgnoreCase("QdbVersionDate")) {
						header.setQdbVersionDate(tempVal);
					} else if (qName.equalsIgnoreCase("PcdbVersionDate")) {
						header.setPcdbVersionDate(tempVal);
					} else if (qName.equalsIgnoreCase("ApprovedFor")) {
						header.setApprovedFor(tempVal);
					} else if (qName.equalsIgnoreCase("DocFormNumber")) {
						header.setDocFormNumber(tempVal);
					} else if (qName.equalsIgnoreCase("MapperPhoneExt")) {
						header.setMapperPhoneExt(tempVal);
					} else if (qName.equalsIgnoreCase("SenderPhoneExt")) {
						header.setSenderPhoneExt(tempVal);
					}
					
					if (qName.equalsIgnoreCase("App")) {
						// add it to the list
						list.add(app);
						//new DBDao().saveAppListRecord(list);
						if((list.size()  == 1000)){
							new DBDao().saveAppListRecord(list);
							list.clear();
							//list = null;
						}/*else if(DBDao.counter >= 2680000){
							new DBDao().saveAppListRecord(list);
							list.clear();
						}*/
						/*else if (DBDao.counter >=50000){
							new DBDao().saveAppListRecord(list);
							list.clear();
							//list = null;
						}*/
						/*else if(DBDao.counter >= 50000) {
							new DBDao().saveAppListRecord(list);
							list.clear();
						}*/
					
					} else if (qName.equalsIgnoreCase("id")) {
						app.setId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("action")) {
						app.setAction(tempVal);
					} else if (qName.equalsIgnoreCase("validate")) {
						app.setValidate(tempVal);
					} else if (qName.equalsIgnoreCase("ref")) {
						app.setRef(tempVal);
					} else if (qName.equalsIgnoreCase("Note")) {
						app.setNote(tempValu + " " + tempVal);
						tempValu = tempValu + tempVal;
					} else if (qName.equalsIgnoreCase("Note lang")) {
						app.setNoteLang(tempVal);
					} else if (qName.equalsIgnoreCase("Qty")) {
						app.setQty(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("PartType")) {
						app.setPartType(tempVal);
					} else if (qName.equalsIgnoreCase("PartType id")) {
						app.setPartTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("Part BrandAAIAID")) {
						app.setPartBrandAAIAId(tempVal);
					} else if(qName.equalsIgnoreCase("Aspiration")) {
						app.setAspiration(tempVal);
					} else if (qName.equalsIgnoreCase("BedLength id")) {
						app.setBedLengthId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("BedType id")) {
						app.setBedTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("BodyNumDoors id")) {
						app.setBodyNumDoorsId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("BodyType id")) {
						app.setBodyTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("BrakeABS id")) {
						app.setBrakeABSId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("BrakeSystem id")) {
						app.setBrakeSystemId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("CylinderHeadType id")) {
						app.setCylinderHeadTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("DriveType")) {
						app.setDriveType(tempVal);
					} else if (qName.equalsIgnoreCase("EngineMfr id")) {
						app.setEngineMfrId(Long.parseLong(tempVal));
					} else if(qName.equalsIgnoreCase("EngineVersion")) {
						app.setEngineVersion(tempVal);
					} else if(qName.equalsIgnoreCase("EngineVIN")) {
						 app.setEngineVIN(tempVal);
					} else if (qName.equalsIgnoreCase("FrontBrakeType id")) {
						app.setFrontBrakeTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("FrontSpringType id")) {
						app.setFrontSpringTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("FuelDeliveryType id")) {
						app.setFuelDeliveryTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("FuelSystemControlType id")) {
						app.setFuelSystemControlTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("FuelSystemDesign id")) {
						app.setFuelSystemDesignId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("FuelType id")) {
						app.setFuelTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("IgnitionSystemType id")) {
						app.setIgnitionSystemTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("Make id")) {
						app.setMakeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("MfrBodyCode id")) {
						app.setMfrBodyCodeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("Model id")) {
						app.setModelId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("PowerOutput id")) {
						app.setPowerOutputId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("RearBrakeType id")) {
						app.setRearBrakeTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("RearSpringType id")) {
						app.setRearSpringTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("Region id")) {
						app.setRegionId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("SteeringType id")) {
						app.setSteeringTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("SteeringSystem id")) {
						app.setSteeringSystemId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("SubModel")) {
						app.setSubModel(tempVal);
					}  else if (qName.equalsIgnoreCase("TransElecControlled id")) {
						app.setTransElecContolledId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("TransmissionMfr id")) {
						app.setTransmissionMfrId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("TransmissionMfrCode id")) {
						app.setTransmissionMfrCodeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("TransmissionBase id")) {
						app.setTransmissionBaseId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("TransmissionControlType id")) {
						app.setTransmissionControlTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("TransmissionNumSpeeds id")) {
						app.setTransmissionNumSpeedsId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("TransmissionType id")) {
						app.setTransmissionTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("ValvesPerEngine id")) {
						app.setValvesPerEngineId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("VehicleType id")) {
						app.setVehicleTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("WheelBase id")) {
						app.setWheelBaseId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("from")) {
						app.setYearsFrom(tempVal);
					} else if (qName.equalsIgnoreCase("to")) {
						app.setYearsTo(tempVal);
					} else if(qName.equalsIgnoreCase("Position")) {
						app.setPosition(tempVal);
					} else if (qName.equalsIgnoreCase("Position id")) {
						app.setPositionId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("Part")) {
						app.setPart(tempVal);
					} else if (qName.equalsIgnoreCase("BaseVehicle")) {
						app.setBaseVehicle(tempVal);
					} else if (qName.equalsIgnoreCase("EngineBase")) {
						app.setEngineBase(tempVal);
					} else if (qName.equalsIgnoreCase("EngineDesignation")) {
						app.setEngineDesignation(tempVal);
					} else if (qName.equalsIgnoreCase("FuelDeliverySubType id")) {
						app.setFuelDeliverySubTypeId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("Note id")) {
						app.setNoteId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("Note lang")) {
						app.setNoteLang(tempVal);
					} else if (qName.equalsIgnoreCase("Qual id")) {
						app.setQualId(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("text")) {
						app.setqPText(tempVal);
					} else if (qName.equalsIgnoreCase("AssetItemOrder")) {
						app.setAssetItemOrder(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("AssetItemRef")) {
						app.setAssetItemRef(tempVal);
					} else if (qName.equalsIgnoreCase("AssetItemName")) {
						app.setAssetItemName(tempVal);
					} else if (qName.equalsIgnoreCase("DisplayOrder")) {
						app.setDisplayOrder(Long.parseLong(tempVal));
					} else if (qName.equalsIgnoreCase("MfrLabel")) {
						app.setMfrLabel(tempVal);
					}
				}				

				@Override
				public void characters(char[] ch, int start, int length)
						throws SAXException {
					tempVal = new String(ch, start, length);
				}

				@Override
				public void warning(SAXParseException e) throws SAXException {
					super.warning(e);
				}

				@Override
				public void error(SAXParseException e) throws SAXException {
					super.error(e);
				}

				@Override
				public void fatalError(SAXParseException e) throws SAXException {
					super.fatalError(e);
				}
				
				
			};
			/*new DBDao().saveAppListRecord(list);
			list.clear();*/
			File folder = new File("E:\\Mamta\\test\\aces");
			//File folder = new File("D:\\Mamta\\New folder\\mk");
			//File folder = new File("D:\\Mamta\\New folder\\xml");
			File[] listOfFiles = folder.listFiles();
		
			for (File list : listOfFiles) {
				//YourClassConstructor(list);
		
				//	System.out.println(list.getName());
					
				//System.out.println("App ID : " +app.getId());
			//		saxParser.parse(list,handler);
			//	new DBDao().saveAppListRecord((List<AppBean>) list);
					//new DBDao().saveAppListRecord((List<AppBean>) list);
				
				//System.out.println("App ID : " +tempApp.getId());
				}
			
		//	saxParser.parse("E:\\Mamta\\test\\ACES_MAHLEOriginal_Filters_20150204.xml", handler);
			saxParser.parse("E:\\Mamta\\test\\xml\\Sealed_Power_ACES_FULL_12-28-2014.xml", handler);
	new DBDao().saveAppListRecord(list);
			
			
		//	saxParser.parse("E:\\Mamta\\test\\xml\\Sealed_Power_ACES_FULL_12-28-2014.xml", handler);
		//	saxParser.parse("E:\\Mamta\\test\\xml\\acesALLTagAndAttributeRead.xml", handler);
	} 
	catch (Exception e) {
			e.printStackTrace();
		}
}
	//new DBDao().saveAppListRecord(list);
public void runExample(){
	parseDocument();
}
	
	public static void main(String argv[]){
		long startTime = System.nanoTime();
		ReadingXMLFile rd = new ReadingXMLFile();
		rd.runExample();
		long endTime = System.nanoTime();
		long elapsedTime = startTime - endTime;
		double seconds = (double)elapsedTime / 1000000000.0;
		System.out.println("Took "+(endTime - startTime) + " ns");
		System.out.println("Took "+(int)seconds + " seconds" );
		}
}

package SAXPARSER;

import java.sql.Connection;
import java.sql.DriverManager;

public class DBConnect {
	private static Connection con;
	private static final String DRIVER_NAME = "oracle.jdbc.driver.OracleDriver";
	private static final String URL = "jdbc:oracle:thin:@192.168.2.68:1521:orcl";
	private static final String USER_NAME = "test";
	private static final String USER_PASSWORD = "test";
	static{
		try {
		Class.forName(DRIVER_NAME);
		con = DriverManager.getConnection(URL, USER_NAME, USER_PASSWORD);
		}
		catch (Exception e) {
		e.printStackTrace();
		}
	}
	public static Connection getConnection(){
		return con;
	}
}
package SAXPARSER;

import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.Statement;
import java.util.List;


public class DBDao {
	
	static int counter = 0, duplicateCounter = 0;
	
	public boolean saveFooterRecord(FooterBean footer){
		boolean status = false;
		Connection con = null;
		PreparedStatement ps = null;
		try {
			con = DBConnect.getConnection();
			String query = "INSERT INTO Footer (FId,R_Count) VALUES (footer_sequence.NEXTVAL,?)";
			ps = con.prepareStatement(query);
			ps.setLong(1, footer.getRecordCount());
			ps.executeUpdate();
			ps.close();
			System.out.println("Record inserted into Footer");
		} catch (Exception e) {
			e.printStackTrace();
		}
		finally {
		   	    if (ps != null) {
		        try {
		            ps.close();
		        } catch (Exception e) { /* ignored */}
		    }
		   /* if (con != null) {
		        try {
		            con.close();
		        } catch (Exception e) {  ignored }
		    }*/
		}
		return status;
	}
	
	public boolean saveHeaderRecord(HeaderBean header){
		boolean status = false;
		Connection con = null;
		PreparedStatement ps = null;
		try {
			con = DBConnect.getConnection();
			String query = "INSERT INTO Header "
				+ "(HId, approvedFor, brandAIAID, company, docFormNumber, documentTitle, effectiveDate,"
				+ " mapperCompany, mapperContact, mapperEmail, mapperPhone, mapperPhoneExt, pcdbVersionDate,"
				+ " qdbVersionDate, senderName, senderPhone, senderPhoneExt, submissionType, transferDate,"
				+ " vcdbVersionDate) VALUES (header_sequence.NEXTVAL, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?,"
				+ " ?, ?, ?, ?, ?, ?)";
			ps = con.prepareStatement(query);
		//	ps.setLong(1, headerId);
			ps.setString(1,(header.getApprovedFor()));
			ps.setString(2,(header.getBrandAAIAID())); 
			ps.setString(3,(header.getCompany())); 
			ps.setString(4,(header.getDocFormNumber())); 
			ps.setString(5,(header.getDocumentTitle())); 
			ps.setString(6,(header.getEffectiveDate())); 
			ps.setString(7,(header.getMapperCompany())); 
			ps.setString(8,(header.getMapperContact())); 
			ps.setString(9,(header.getMapperEmail())); 
			ps.setString(10,(header.getMapperPhone())); 
			ps.setString(11,(header.getMapperPhoneExt())); 
			ps.setString(12,(header.getPcdbVersionDate())); 
			ps.setString(13,(header.getQdbVersionDate())); 
			ps.setString(14,(header.getSenderName())); 
			ps.setString(15,(header.getSenderPhone())); 
			ps.setString(16,(header.getSenderPhoneExt())); 
			ps.setString(17,(header.getSubmissionType())); 
			ps.setString(18,(header.getTransferDate())); 
			ps.setString(19,(header.getVcdbVersionDate())); 
			ps.executeUpdate();
			System.out.println("Record inserted into Header");
		} catch (Exception e) {
			e.printStackTrace();
		}finally {
		    if (ps != null) {
		        try {
		            ps.close();
		        } catch (Exception e) { /* ignored */}
		    }
		   /* if (con != null) {
		        try {
		            con.close();
		        } catch (Exception e) {  ignored }
		    }*/
		}
		return status;
	}

	public boolean saveAppListRecord(List<AppBean> list){
		boolean status = false;	
		Connection con = null;
		PreparedStatement ps = null;
		int s = 0;
		int head = 0;
		int s1 = 0;
		int foot = 0;
		ResultSet rs = null;
		ResultSet rs1 = null;
		//final int batchSize = 1000;
	//	int count = 0;
		try {
			con = DBConnect.getConnection();
			String query = "INSERT INTO App (APID, action, id, ref, aValidate, aspiration, aspirationId , assetAction, assetId, assetRef,"
					+ " assetValidate, assetItemOrder, assetItemRef, assetItemName, baseVehicle, baseVehicleId, bedLengthId, bedTypeId,"
					+ " bodyNumDoorsId, bodyTypeId, brakeABSId, brakeSystemId, cylinderHeadTypeId, displayOrder, driveTypeId, engineBase,"
					+ " engineBaseId, engineDesignation, engineDesignationId, engineMfrId, engineVersion, engineVersionId, engineVIN,"
					+ " engineVINId, frontBrakeTypeId, frontSpringTypeId, fuelDeliverySubTypeId, fuelDeliveryTypeId, fuelSystemControlTypeId,"
					+ " fuelSystemDesignId, fuelTypeId, ignitionSystemTypeId, makeId, mfrLabel, mfrBodyCodeId, modelId, note, noteId, noteLang,"
					+ " part, partBrandAAIAId, partType, partTypeId, position, positionId, powerOutputId, qualId, qParamUom, qParamValue,"
					+ " qParamAltValue, qParamAltUom, qPText, qty, rearBrakeTypeId, rearSpringTypeId, regionId, steeringTypeId,"
					+ " steeringSystemId, subModel, subModelId, transElecContolledId, transmissionMfrId, transmissionMfrCodeId,"
					+ " transmissionBaseId, transmissionControlTypeId, transmissionNumSpeedsId, transmissionTypeId, valvesPerEngineId,"
					+ " vehicleTypeId, wheelBaseId, yearsFrom, yearsTo, driveType, headerId, footerId) VALUES (app_sequence.NEXTVAL, ?, ?,"
					+ " ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?,"
					+ " ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?,"
					+ " ?, ?, ?, ?, ?, ?) ";
			ps = con.prepareStatement(query);
			rs = con.createStatement().executeQuery("select MAX(HId) from Header");
			if (rs != null) {
				while (rs.next()) {
					head = rs.getInt(1);
				}
				rs.close();
			}
			s = head;
			rs1 = con.createStatement()
					.executeQuery("select MAX(FID) from Footer");
			if (rs1 != null) {
				while (rs1.next()) {
					//foot = rs1.getInt(1);
					foot = (rs1.getInt(1)+1);
				}
				rs1.close();
			}
			s1 = foot;
			for(AppBean app : list){
				if(!toExitRecord(app)){
					ps.setString(1, (app.getAction()));
					ps.setLong(2, (app.getId()));
					ps.setString(3, (app.getRef()));
					ps.setString(4, (app.getValidate()));
					ps.setString(5, (app.getAspiration()));
					ps.setLong(6, (app.getAspirationId()));
					ps.setString(7, (app.getAssetAction()));
					ps.setLong(8, (app.getAssetId()));
					ps.setString(9, (app.getAssetRef()));
					ps.setString(10, (app.getAssetValidate()));
					ps.setLong(11, (app.getAssetItemOrder()));
					ps.setString(12, (app.getAssetItemRef()));
					ps.setString(13, (app.getAssetItemName()));
					ps.setString(14, (app.getBaseVehicle()));
					ps.setLong(15, (app.getBaseVehicleId()));
					ps.setLong(16, (app.getBedLengthId()));
					ps.setLong(17, (app.getBedTypeId()));
					ps.setLong(18, (app.getBodyNumDoorsId()));
					ps.setLong(19, (app.getBodyTypeId()));
					ps.setLong(20, (app.getBrakeABSId()));
					ps.setLong(21, (app.getBrakeSystemId()));
					ps.setLong(22, (app.getCylinderHeadTypeId()));
					ps.setLong(23, (app.getDisplayOrder()));
					ps.setLong(24, (app.getDriveTypeId()));
					ps.setString(25, (app.getEngineBase()));
					ps.setLong(26, (app.getEngineBaseId()));
					ps.setString(27, (app.getEngineDesignation()));
					ps.setLong(28, (app.getEngineDesignationId()));
					ps.setLong(29, (app.getEngineMfrId()));
					ps.setString(30, (app.getEngineVersion()));
					ps.setLong(31, (app.getEngineVersionId()));
					ps.setString(32, (app.getEngineVIN()));
					ps.setLong(33, (app.getEngineVINId()));
					ps.setLong(34, (app.getFrontBrakeTypeId()));
					ps.setLong(35, (app.getFrontSpringTypeId()));
					ps.setLong(36, (app.getFuelDeliverySubTypeId()));
					ps.setLong(37, (app.getFuelDeliveryTypeId()));
					ps.setLong(38, (app.getFuelSystemControlTypeId()));
					ps.setLong(39, (app.getFuelSystemDesignId()));
					ps.setLong(40, (app.getFuelTypeId()));
					ps.setLong(41, (app.getIgnitionSystemTypeId()));
					ps.setLong(42, (app.getMakeId()));
					ps.setString(43, (app.getMfrLabel()));
					ps.setLong(44, (app.getMfrBodyCodeId()));
					ps.setLong(45, (app.getModelId()));
					ps.setString(46, (app.getNote()));
					ps.setLong(47, (app.getNoteId()));
					ps.setString(48, (app.getNoteLang()));
					ps.setString(49, (app.getPart()));
					ps.setString(50, (app.getPartBrandAAIAId()));
					ps.setString(51, (app.getPartType()));
					ps.setLong(52, (app.getPartTypeId()));
					ps.setString(53, (app.getPosition()));
					ps.setLong(54, (app.getPositionId()));
					ps.setLong(55, (app.getPowerOutputId()));
					ps.setLong(56, (app.getQualId()));
					ps.setString(57, (app.getqParamUom()));
					ps.setString(58, (app.getqParamValue()));
					ps.setString(59, (app.getqParamAltValue()));
					ps.setString(60, (app.getqParamAltUom()));
					ps.setString(61, (app.getqPText()));
					ps.setLong(62, (app.getQty()));
					ps.setLong(63, (app.getRearBrakeTypeId()));
					ps.setLong(64, (app.getRearSpringTypeId()));
					ps.setLong(65, (app.getRegionId()));
					ps.setLong(66, (app.getSteeringTypeId()));
					ps.setLong(67, (app.getSteeringSystemId()));
					ps.setString(68, (app.getSubModel()));
					ps.setLong(69, (app.getSubModelId()));
					ps.setLong(70, (app.getTransElecContolledId()));
					ps.setLong(71, (app.getTransmissionMfrId()));
					ps.setLong(72, (app.getTransmissionMfrCodeId()));
					ps.setLong(73, (app.getTransmissionBaseId()));
					ps.setLong(74, (app.getTransmissionControlTypeId()));
					ps.setLong(75, (app.getTransmissionNumSpeedsId()));
					ps.setLong(76, (app.getTransmissionTypeId()));
					ps.setLong(77, (app.getValvesPerEngineId()));
					ps.setLong(78, (app.getVehicleTypeId()));
					ps.setLong(79, (app.getWheelBaseId()));
					ps.setString(80, (app.getYearsFrom()));
					ps.setString(81, (app.getYearsTo()));
					ps.setString(82, (app.getDriveType()));
					ps.setLong(83, s);
					ps.setLong(84, s1);
					ps.addBatch();
					/* if(++count % batchSize == 0) {
					        ps.executeBatch();
					    }*/
					++counter;
				 }	
			}
			ps.executeBatch();
			//ps.executeUpdate();
			System.out.println("Record inserted into App    " + counter);
			ps.close();
		} catch (Exception e) {
			e.printStackTrace();
		}finally {
		    if (rs != null) {
		        try {
		            rs.close();
		        } catch (Exception e) { /* ignored */}
		    }
		    if (ps != null) {
		        try {
		            ps.close();
		        } catch (Exception e) { /* ignored */}
		    }
		    /*if (con != null) {
		        try {
		            con.close();
		        } catch (Exception e) {  ignored }
		    }*/
		}
		return status;
	}
	public boolean toExitRecord(AppBean app){
		boolean status = false;
		Connection con = null;
		Statement stmt = null;
		ResultSet rs = null;
		try{
			con = DBConnect.getConnection();
			stmt = con.createStatement();
			String storeSql = "SELECT action, id, ref, aValidate, aspiration, aspirationId , assetAction, assetId, assetRef, assetValidate,"
					+ " assetItemOrder, assetItemRef, assetItemName, baseVehicle, baseVehicleId, bedLengthId, bedTypeId, bodyNumDoorsId,"
					+ " bodyTypeId, brakeABSId, brakeSystemId, cylinderHeadTypeId, displayOrder, driveTypeId, engineBase, engineBaseId,"
					+ " engineDesignation, engineDesignationId, engineMfrId, engineVersion, engineVersionId, engineVIN, engineVINId,"
					+ " frontBrakeTypeId, frontSpringTypeId, fuelDeliverySubTypeId, fuelDeliveryTypeId, fuelSystemControlTypeId,"
					+ " fuelSystemDesignId, fuelTypeId, ignitionSystemTypeId, makeId, mfrLabel, mfrBodyCodeId, modelId, note, noteId, noteLang,"
					+ " part, partBrandAAIAId, partType, partTypeId, position, positionId, powerOutputId, qualId, qParamUom, qParamValue,"
					+ " qParamAltValue, qParamAltUom, qPText, qty, rearBrakeTypeId, rearSpringTypeId, regionId, steeringTypeId, steeringSystemId,"
					+ " subModel, subModelId, transElecContolledId, transmissionMfrId, transmissionMfrCodeId, transmissionBaseId,"
					+ " transmissionControlTypeId, transmissionNumSpeedsId, transmissionTypeId, valvesPerEngineId, vehicleTypeId, wheelBaseId,"
					+ " yearsFrom, yearsTo, driveType From App where ";
			if(app.getAction() != null && !"".equals(app.getAction().trim()))
				 storeSql +=" action = '"+app.getAction()+"'";
			if(app.getId() != 0)
				 storeSql +=" and id = "+app.getId();
			if(app.getRef() != null && 	!"".equals(app.getRef().trim()))
				 storeSql +=" and ref = '"+app.getRef()+"'";
			if(app.getValidate() != null && !"".equals(app.getValidate().trim()))
				 storeSql +=" and aValidate = '"+app.getValidate()+"'";
			if(app.getAspiration() != null && !"".equals(app.getAspiration().trim()))
				 storeSql +=" and aspiration = '"+app.getAspiration()+"'";
			if(app.getAspirationId() != 0)
				 storeSql +=" and aspirationId = "+app.getAspirationId();
			if(app.getAssetAction() != null && !"".equals(app.getAssetAction().trim()))
				 storeSql +=" and assetAction = '"+app.getAssetAction()+"'";
			if(app.getAssetId() != 0)
				 storeSql +=" and assetId = "+app.getAssetId();
			if(app.getAssetRef() != null && !"".equals(app.getAssetRef().trim()))
				 storeSql +=" and assetRef = '"+app.getAssetRef()+"'";
			if(app.getAssetValidate() != null && !"".equals(app.getAssetValidate()))
				 storeSql +=" and assetValidate = '"+app.getAssetValidate()+"'";
			if(app.getAssetItemOrder() != 0)
				 storeSql +=" and assetItemOrder = "+app.getAssetItemOrder();
			if(app.getAssetItemRef() != null && !"".equals(app.getAssetItemRef().trim()))
				 storeSql +=" and assetItemRef = '"+app.getAssetItemRef()+"'";
			if(app.getAssetItemName() != null && !"".equals(app.getAssetItemName().trim()))
				 storeSql +=" and assetItemName = '"+app.getAssetItemName()+"'";
			if(app.getBaseVehicle() != null && !"".equals(app.getBaseVehicle().trim()))
				 storeSql +=" and baseVehicle = '"+app.getBaseVehicle()+"'";
			if(app.getBaseVehicleId() != 0)
				 storeSql +=" and baseVehicleId = "+app.getBaseVehicleId();  
			if(app.getBedLengthId() != 0)
				 storeSql +=" and bedLengthId = "+app.getBedLengthId();
			if(app.getBedTypeId() != 0)
				 storeSql +=" and bedTypeId = "+app.getBedTypeId();
			if(app.getBodyNumDoorsId() != 0)
				 storeSql +=" and bodyNumDoorsId = "+app.getBodyNumDoorsId();
			if(app.getBodyTypeId() != 0)
				 storeSql +=" and bodyTypeId = "+app.getBodyTypeId();
			if(app.getBrakeABSId() != 0)
				 storeSql +=" and brakeABSId = "+app.getBrakeABSId();
			if(app.getBrakeSystemId() != 0)
				 storeSql +=" and brakeSystemId = "+app.getBrakeSystemId();
			if(app.getCylinderHeadTypeId() != 0)
				 storeSql +=" and cylinderHeadTypeId = "+app.getCylinderHeadTypeId();
			if(app.getDisplayOrder() != 0)
				 storeSql +=" and displayOrder = "+app.getDisplayOrder();
			if(app.getDriveTypeId() != 0)
				 storeSql +=" and driveTypeId = "+app.getDriveTypeId();
			if(app.getEngineBase() != null && !"".equals(app.getEngineBase().trim()))
				 storeSql +=" and engineBase = '"+app.getEngineBase()+"'";
			if(app.getEngineBaseId()  != 0)
				 storeSql +=" and engineBaseId = "+app.getEngineBaseId();
			if(app.getEngineDesignation() != null && !"".equals(app.getEngineDesignation().trim()))
				 storeSql +=" and engineDesignation = '"+app.getEngineDesignation()+"'";
			if(app.getEngineDesignationId() != 0)
				 storeSql +=" and engineDesignationId = "+app.getEngineDesignationId();
			if(app.getEngineMfrId() != 0)
				 storeSql +=" and engineMfrId = "+app.getEngineMfrId();
			if(app.getEngineVersion() != null && !"".equals(app.getEngineVersion().trim()))
				 storeSql +=" and engineVersion = '"+app.getEngineVersion()+"'";
			if(app.getEngineVersionId() != 0)
				 storeSql +=" and engineVersionId = "+app.getEngineVersionId();
			if(app.getEngineVIN() != null  && !"".equals(app.getEngineVIN().trim()))
				 storeSql +=" and engineVIN = '"+app.getEngineVIN()+"'";
			if(app.getEngineVINId() != 0)
				 storeSql +=" and engineVINId = "+app.getEngineVINId();
			if(app.getFrontBrakeTypeId() != 0)
				 storeSql +=" and frontBrakeTypeId = "+app.getFrontBrakeTypeId();
			if(app.getFrontSpringTypeId() != 0)
				 storeSql +=" and frontSpringTypeId = "+app.getFrontSpringTypeId();
			if(app.getFuelDeliverySubTypeId() != 0)
				 storeSql +=" and fuelDeliverySubTypeId = "+app.getFuelDeliverySubTypeId();
			if(app.getFuelDeliveryTypeId() != 0)
				 storeSql +=" and fuelDeliveryTypeId = "+app.getFuelDeliveryTypeId();
			if(app.getFuelSystemControlTypeId() != 0)
				 storeSql +=" and fuelSystemControlTypeId = "+app.getFuelSystemControlTypeId();
			if(app.getFuelSystemDesignId() != 0)
				 storeSql +=" and fuelSystemDesignId = "+app.getFuelSystemDesignId();
			if(app.getFuelTypeId() != 0)
				 storeSql +=" and fuelTypeId = "+app.getFuelTypeId();
			if(app.getIgnitionSystemTypeId() != 0)
				 storeSql +=" and ignitionSystemTypeId = "+app.getIgnitionSystemTypeId();
			if(app.getMakeId() != 0)
				 storeSql +=" and makeId = "+app.getMakeId();
			if(app.getMfrLabel() != null && !"".equals(app.getMfrLabel().trim()))
				 storeSql +=" and mfrLabel = '"+app.getMfrLabel()+"'";
			if(app.getMfrBodyCodeId() != 0)
				 storeSql +=" and mfrBodyCodeId = "+app.getMfrBodyCodeId();
			if(app.getModelId() != 0)
				 storeSql +=" and modelId = "+app.getModelId();
			if(app.getNote() != null && !"".equals(app.getNote().trim()))
				 storeSql +=" and note = '"+app.getNote()+"'";
			if(app.getNoteId() != 0)
				 storeSql +=" and noteId = "+app.getNoteId();
			if(app.getNoteLang() != null && !"".equals(app.getNoteLang().trim()))
				 storeSql +=" and noteLang = '"+app.getNoteLang()+"'";
			if(app.getPart() != null && !"".equals(app.getPart().trim()))
				 storeSql +=" and part = '"+app.getPart()+"'";
			if(app.getPartBrandAAIAId() != null && !"".equals(app.getPartBrandAAIAId().trim()))
				 storeSql +=" and partBrandAAIAId = '"+app.getPartBrandAAIAId()+"'";
			if(app.getPartType() != null  && !"".equals(app.getPartType().trim()))
				 storeSql +=" and partType = '"+app.getPartType()+"'";
			if(app.getPartTypeId() != 0)
				 storeSql +=" and partTypeId = "+app.getPartTypeId();
			if(app.getPosition() != null  && !"".equals(app.getPosition().trim()))
				 storeSql +=" and position = '"+app.getPosition()+"'";
			if(app.getPositionId() != 0)
				 storeSql +=" and positionId = "+app.getPositionId();
			if(app.getPowerOutputId() != 0)
				 storeSql +=" and powerOutputId = "+app.getPowerOutputId();
			if(app.getQualId() != 0)
				 storeSql +=" and qualId = "+app.getQualId();
			if(app.getqParamUom() != null  && !"".equals(app.getqParamAltUom().trim()))
				 storeSql +=" and qParamUom = '"+app.getqParamUom()+"'";
			if(app.getqParamValue() != null  && !"".equals(app.getqParamValue().trim()))
				 storeSql +=" and qParamValue = '"+app.getqParamValue()+"'";
			if(app.getqParamAltValue() != null && !"".equals(app.getqParamAltValue().trim()))
				 storeSql +=" and qParamAltValue = '"+app.getqParamAltValue()+"'";
			if(app.getqParamAltUom() != null && !"".equals(app.getqParamAltUom().trim()))
				 storeSql +=" and qParamAltUom = '"+app.getqParamAltUom()+"'";
			if(app.getqPText() != null && !"".equals(app.getqPText().trim()))
				 storeSql +=" and qPText = '"+app.getqPText()+"'";
			if(app.getQty() != 0)
				 storeSql +=" and qty = "+app.getQty();
			if(app.getRearBrakeTypeId() != 0)
				 storeSql +=" and rearBrakeTypeId= "+app.getRearBrakeTypeId();
			if(app.getRearSpringTypeId() != 0)
				 storeSql +=" and rearSpringTypeId = "+app.getRearSpringTypeId();
			if(app.getRegionId() != 0)
				 storeSql +=" and regionId = "+app.getRegionId();
			if(app.getSteeringTypeId() != 0)
				 storeSql +=" and steeringTypeId = "+app.getSteeringTypeId();
			if(app.getSteeringSystemId() != 0)
				 storeSql +=" and steeringSystemId = "+app.getSteeringSystemId();
			if(app.getSubModel() != null && !"".equals(app.getSubModel().trim()))
				 storeSql +=" and subModel = '"+app.getSubModel()+"'";
			if(app.getSubModelId() != 0)
				 storeSql +=" and subModelId = "+app.getSubModelId();
			if(app.getTransElecContolledId() != 0)
				 storeSql +=" and transElecContolledId = "+app.getTransElecContolledId();
			if(app.getTransmissionMfrId() != 0)
				 storeSql +=" and transmissionMfrId = "+app.getTransmissionMfrId();
			if(app.getTransmissionMfrCodeId() != 0)
				 storeSql +=" and transmissionMfrCodeId = "+app.getTransmissionMfrCodeId();
			if(app.getTransmissionBaseId() != 0)
				 storeSql +=" and transmissionBaseId = "+app.getTransmissionBaseId();
			if(app.getTransmissionControlTypeId() != 0)
				 storeSql +=" and transmissionControlTypeId = "+app.getTransmissionControlTypeId();
			if(app.getTransmissionNumSpeedsId() != 0)
				 storeSql +=" and transmissionNumSpeedsId = "+app.getTransmissionNumSpeedsId();
			if(app.getTransmissionTypeId() != 0)
				 storeSql +=" and transmissionTypeId = "+app.getTransmissionTypeId();
			if(app.getValvesPerEngineId() != 0)
				 storeSql +=" and valvesPerEngineId = "+app.getValvesPerEngineId();
			if(app.getVehicleTypeId() != 0)
				 storeSql +=" and vehicleTypeId = "+app.getVehicleTypeId();
			if(app.getWheelBaseId() != 0)
				 storeSql +=" and wheelBaseId = "+app.getWheelBaseId();
			if(app.getYearsFrom() != null && !"".equals(app.getYearsFrom().trim()))
				 storeSql +=" and yearsFrom = '"+app.getYearsFrom()+"'";
			if(app.getYearsTo() != null && !"".equals(app.getYearsTo().trim()))
				 storeSql +=" and yearsTo = '"+app.getYearsTo()+"'";
			if(app.getDriveType() != null && !"".equals(app.getDriveType().trim()))
				 storeSql +=" and driveType = '"+app.getDriveType()+"'";
			
			rs = stmt.executeQuery(storeSql);
			if(rs.next()){
				status = true;
				++duplicateCounter;
				rs.close();
			}
			System.out.println("Duplicate records  ..... "+ duplicateCounter);
			rs.close();
			stmt.close();
			
		}catch(Exception e){
			e.printStackTrace();
		}
		finally {
			 try {
				 stmt.close();
		        } catch (Exception e) { /* ignored */}
		    
		   	    if (rs != null) {
		        try {
		            rs.close();
		        } catch (Exception e) { /* ignored */}
		    }
//		    if (con != null) {
//		        try {
//		            con.close();
//		        } catch (Exception e) { /* ignored */}
//		    }
		}
		
		return status;
	}
}

package SAXPARSER;

public class FooterBean {
	private long fPId;
	private long recordCount;
	public FooterBean() {
	super();
	}
	public FooterBean(long fPId, long recordCount) {
	super();
	this.fPId = fPId;
	this.recordCount = recordCount;
	}
	public long getfPId() {
	return fPId;
	}
	public void setfPId(long fPId) {
	this.fPId = fPId;
	}
	public long getRecordCount() {
	return recordCount;
	}
	public void setRecordCount(long recordCount) {
	this.recordCount = recordCount;
	}
	@Override
	public String toString() {
	return "Footer [fPId=" + fPId + ", recordCount=" + recordCount + "]";
	}
}


package SAXPARSER;

public class HeaderBean {
	private long hPId;
	private String approvedFor;
	private String brandAAIAID;
	private String company;
	private String docFormNumber;
	private String documentTitle;
	private String effectiveDate;
	private String mapperCompany;
	private String mapperContact;
	private String mapperEmail;
	private String mapperPhone;
	private String mapperPhoneExt;
	private String pcdbVersionDate;
	private String qdbVersionDate;
	private String senderName;
	private String senderPhone;
	private String senderPhoneExt;
	private String submissionType;
	private String transferDate;
	private String vcdbVersionDate;
	public HeaderBean() {
	super();
	}
	public HeaderBean(long hPId, String approvedFor, String brandAAIAID,
	String company, String docFormNumber, String documentTitle,
	String effectiveDate, String mapperCompany, String mapperContact,
	String mapperEmail, String mapperPhone, String mapperPhoneExt,
	String pcdbVersionDate, String qdbVersionDate, String senderName,
	String senderPhone, String senderPhoneExt, String submissionType,
	String transferDate, String vcdbVersionDate) {
	super();
	this.hPId = hPId;
	this.approvedFor = approvedFor;
	this.brandAAIAID = brandAAIAID;
	this.company = company;
	this.docFormNumber = docFormNumber;
	this.documentTitle = documentTitle;
	this.effectiveDate = effectiveDate;
	this.mapperCompany = mapperCompany;
	this.mapperContact = mapperContact;
	this.mapperEmail = mapperEmail;
	this.mapperPhone = mapperPhone;
	this.mapperPhoneExt = mapperPhoneExt;
	this.pcdbVersionDate = pcdbVersionDate;
	this.qdbVersionDate = qdbVersionDate;
	this.senderName = senderName;
	this.senderPhone = senderPhone;
	this.senderPhoneExt = senderPhoneExt;
	this.submissionType = submissionType;
	this.transferDate = transferDate;
	this.vcdbVersionDate = vcdbVersionDate;
	}
	public long gethPId() {
	return hPId;
	}
	public void sethPId(long hPId) {
	this.hPId = hPId;
	}
	public String getApprovedFor() {
	return approvedFor;
	}
	public void setApprovedFor(String approvedFor) {
	this.approvedFor = approvedFor;
	}
	public String getBrandAAIAID() {
	return brandAAIAID;
	}
	public void setBrandAAIAID(String brandAAIAID) {
	this.brandAAIAID = brandAAIAID;
	}
	public String getCompany() {
	return company;
	}
	public void setCompany(String company) {
	this.company = company;
	}
	public String getDocFormNumber() {
	return docFormNumber;
	}
	public void setDocFormNumber(String docFormNumber) {
	this.docFormNumber = docFormNumber;
	}
	public String getDocumentTitle() {
	return documentTitle;
	}
	public void setDocumentTitle(String documentTitle) {
	this.documentTitle = documentTitle;
	}
	public String getEffectiveDate() {
	return effectiveDate;
	}
	public void setEffectiveDate(String effectiveDate) {
	this.effectiveDate = effectiveDate;
	}
	public String getMapperCompany() {
	return mapperCompany;
	}
	public void setMapperCompany(String mapperCompany) {
	this.mapperCompany = mapperCompany;
	}
	public String getMapperContact() {
	return mapperContact;
	}
	public void setMapperContact(String mapperContact) {
	this.mapperContact = mapperContact;
	}
	public String getMapperEmail() {
	return mapperEmail;
	}
	public void setMapperEmail(String mapperEmail) {
	this.mapperEmail = mapperEmail;
	}
	public String getMapperPhone() {
	return mapperPhone;
	}
	public void setMapperPhone(String mapperPhone) {
	this.mapperPhone = mapperPhone;
	}
	public String getMapperPhoneExt() {
	return mapperPhoneExt;
	}
	public void setMapperPhoneExt(String mapperPhoneExt) {
	this.mapperPhoneExt = mapperPhoneExt;
	}
	public String getPcdbVersionDate() {
	return pcdbVersionDate;
	}
	public void setPcdbVersionDate(String pcdbVersionDate) {
	this.pcdbVersionDate = pcdbVersionDate;
	}
	public String getQdbVersionDate() {
	return qdbVersionDate;
	}
	public void setQdbVersionDate(String qdbVersionDate) {
	this.qdbVersionDate = qdbVersionDate;
	}
	public String getSenderName() {
	return senderName;
	}
	public void setSenderName(String senderName) {
	this.senderName = senderName;
	}
	public String getSenderPhone() {
	return senderPhone;
	}
	public void setSenderPhone(String senderPhone) {
	this.senderPhone = senderPhone;
	}
	public String getSenderPhoneExt() {
	return senderPhoneExt;
	}
	public void setSenderPhoneExt(String senderPhoneExt) {
	this.senderPhoneExt = senderPhoneExt;
	}
	public String getSubmissionType() {
	return submissionType;
	}
	public void setSubmissionType(String submissionType) {
	this.submissionType = submissionType;
	}
	public String getTransferDate() {
	return transferDate;
	}
	public void setTransferDate(String transferDate) {
	this.transferDate = transferDate;
	}
	public String getVcdbVersionDate() {
	return vcdbVersionDate;
	}
	public void setVcdbVersionDate(String vcdbVersionDate) {
	this.vcdbVersionDate = vcdbVersionDate;
	}
	@Override
	public String toString() {
	return "Header [hPId=" + hPId + ", approvedFor=" + approvedFor
	+ ", brandAAIAID=" + brandAAIAID + ", company=" + company
	+ ", docFormNumber=" + docFormNumber + ", documentTitle="
	+ documentTitle + ", effectiveDate=" + effectiveDate
	+ ", mapperCompany=" + mapperCompany + ", mapperContact="
	+ mapperContact + ", mapperEmail=" + mapperEmail
	+ ", mapperPhone=" + mapperPhone + ", mapperPhoneExt="
	+ mapperPhoneExt + ", pcdbVersionDate=" + pcdbVersionDate
	+ ", qdbVersionDate=" + qdbVersionDate + ", senderName="
	+ senderName + ", senderPhone=" + senderPhone
	+ ", senderPhoneExt=" + senderPhoneExt + ", submissionType="
	+ submissionType + ", transferDate=" + transferDate
	+ ", vcdbVersionDate=" + vcdbVersionDate + "]";
	}
}


package SAXPARSER;

public class AppBean {
	private long aPId;
	private String action;
	private long id;
	private String aspiration;
	private long aspirationId;
	private String assetAction;
	private long assetId;
	private String assetRef;
	private String assetValidate;
	private String ref;
	private String validate;
	private long assetItemOrder;
	private String assetItemRef;
	private String assetItemName;
	private String baseVehicle;
	private long baseVehicleId;
	private long bedLengthId;
	private long bedTypeId;
	private long bodyNumDoorsId;
	private long bodyTypeId;
	private long brakeABSId;
	private long brakeSystemId;
	private long cylinderHeadTypeId;
	private long displayOrder;
	private long driveTypeId;
	private String engineBase;
	private long engineBaseId;
	private String engineDesignation;
	private long engineDesignationId;
	private long engineMfrId;
	private String engineVersion;
	private long engineVersionId;
	private String engineVIN;
	private long engineVINId;
	private long frontBrakeTypeId;
	private long frontSpringTypeId;
	private long fuelDeliverySubTypeId;
	private long fuelDeliveryTypeId;
	private long fuelSystemControlTypeId;
	private long fuelSystemDesignId;
	private long fuelTypeId;
	private long ignitionSystemTypeId;
	private long makeId;
	private String mfrLabel;
	private long mfrBodyCodeId;
	private long modelId;
	private String note;
	private long noteId;
	private String noteLang;
	private String part;
	private String partBrandAAIAId;
	private String partType;
	private long partTypeId;
	private String position;
	private long positionId;
	private long powerOutputId;
	private long qualId;
	private String qParamUom;
	private String qParamValue;
	private String qParamAltValue;
	private String qParamAltUom;
	private String qPText;
	private long qty;
	private long rearBrakeTypeId;
	private long rearSpringTypeId;
	private long regionId;
	private long steeringTypeId;
	private long steeringSystemId;
	private String subModel;
	private long subModelId;
	private long transElecContolledId;
	private long transmissionMfrId;
	private long transmissionMfrCodeId;
	private long transmissionBaseId;
	private long transmissionControlTypeId;
	private long transmissionNumSpeedsId;
	private long transmissionTypeId;
	private long valvesPerEngineId;
	private long vehicleTypeId;
	private long wheelBaseId;
	private String yearsFrom;
	private String yearsTo;
	private String driveType;
	public AppBean() {
		super();
	}
	public AppBean(long aPId, String action, long id, String aspiration,
		long aspirationId, String assetAction, long assetId,
		String assetRef, String assetValidate, String ref, String validate,
		long assetItemOrder, String assetItemRef, String assetItemName,
		String baseVehicle, long baseVehicleId, long bedLengthId,
		long bedTypeId, long bodyNumDoorsId, long bodyTypeId,
		long brakeABSId, long brakeSystemId, long cylinderHeadTypeId,
		long displayOrder, long driveTypeId, String engineBase,
		long engineBaseId, String engineDesignation,
		long engineDesignationId, long engineMfrId, String engineVersion,
		long engineVersionId, String engineVIN, long engineVINId,
		long frontBrakeTypeId, long frontSpringTypeId,
		long fuelDeliverySubTypeId, long fuelDeliveryTypeId,
		long fuelSystemControlTypeId, long fuelSystemDesignId,
		long fuelTypeId, long ignitionSystemTypeId, long makeId,
		String mfrLabel, long mfrBodyCodeId, long modelId, String note,
		long noteId, String noteLang, String part, String partBrandAAIAId,
		String partType, long partTypeId, String position, long positionId,
		long powerOutputId, long qualId, String qParamUom,
		String qParamValue, String qParamAltValue, String qParamAltUom,
		String qPText, long qty, long rearBrakeTypeId,
		long rearSpringTypeId, long regionId, long steeringTypeId,
		long steeringSystemId, String subModel, long subModelId,
		long transElecContolledId, long transmissionMfrId,
		long transmissionMfrCodeId, long transmissionBaseId,
		long transmissionControlTypeId, long transmissionNumSpeedsId,
		long transmissionTypeId, long valvesPerEngineId,
		long vehicleTypeId, long wheelBaseId, String yearsFrom,
		String yearsTo, String driveType) {
			super();
			this.aPId = aPId;
			this.action = action;
			this.id = id;
			this.aspiration = aspiration;
			this.aspirationId = aspirationId;
			this.assetAction = assetAction;
			this.assetId = assetId;
			this.assetRef = assetRef;
			this.assetValidate = assetValidate;
			this.ref = ref;
			this.validate = validate;
			this.assetItemOrder = assetItemOrder;
			this.assetItemRef = assetItemRef;
			this.assetItemName = assetItemName;
			this.baseVehicle = baseVehicle;
			this.baseVehicleId = baseVehicleId;
			this.bedLengthId = bedLengthId;
			this.bedTypeId = bedTypeId;
			this.bodyNumDoorsId = bodyNumDoorsId;
			this.bodyTypeId = bodyTypeId;
			this.brakeABSId = brakeABSId;
			this.brakeSystemId = brakeSystemId;
			this.cylinderHeadTypeId = cylinderHeadTypeId;
			this.displayOrder = displayOrder;
			this.driveTypeId = driveTypeId;
			this.engineBase = engineBase;
			this.engineBaseId = engineBaseId;
			this.engineDesignation = engineDesignation;
			this.engineDesignationId = engineDesignationId;
			this.engineMfrId = engineMfrId;
			this.engineVersion = engineVersion;
			this.engineVersionId = engineVersionId;
			this.engineVIN = engineVIN;
			this.engineVINId = engineVINId;
			this.frontBrakeTypeId = frontBrakeTypeId;
			this.frontSpringTypeId = frontSpringTypeId;
			this.fuelDeliverySubTypeId = fuelDeliverySubTypeId;
			this.fuelDeliveryTypeId = fuelDeliveryTypeId;
			this.fuelSystemControlTypeId = fuelSystemControlTypeId;
			this.fuelSystemDesignId = fuelSystemDesignId;
			this.fuelTypeId = fuelTypeId;
			this.ignitionSystemTypeId = ignitionSystemTypeId;
			this.makeId = makeId;
			this.mfrLabel = mfrLabel;
			this.mfrBodyCodeId = mfrBodyCodeId;
			this.modelId = modelId;
			this.note = note;
			this.noteId = noteId;
			this.noteLang = noteLang;
			this.part = part;
			this.partBrandAAIAId = partBrandAAIAId;
			this.partType = partType;
			this.partTypeId = partTypeId;
			this.position = position;
			this.positionId = positionId;
			this.powerOutputId = powerOutputId;
			this.qualId = qualId;
			this.qParamUom = qParamUom;
			this.qParamValue = qParamValue;
			this.qParamAltValue = qParamAltValue;
			this.qParamAltUom = qParamAltUom;
			this.qPText = qPText;
			this.qty = qty;
			this.rearBrakeTypeId = rearBrakeTypeId;
			this.rearSpringTypeId = rearSpringTypeId;
			this.regionId = regionId;
			this.steeringTypeId = steeringTypeId;
			this.steeringSystemId = steeringSystemId;
			this.subModel = subModel;
			this.subModelId = subModelId;
			this.transElecContolledId = transElecContolledId;
			this.transmissionMfrId = transmissionMfrId;
			this.transmissionMfrCodeId = transmissionMfrCodeId;
			this.transmissionBaseId = transmissionBaseId;
			this.transmissionControlTypeId = transmissionControlTypeId;
			this.transmissionNumSpeedsId = transmissionNumSpeedsId;
			this.transmissionTypeId = transmissionTypeId;
			this.valvesPerEngineId = valvesPerEngineId;
			this.vehicleTypeId = vehicleTypeId;
			this.wheelBaseId = wheelBaseId;
			this.yearsFrom = yearsFrom;
			this.yearsTo = yearsTo;
			this.driveType = driveType;
		}
		public long getaPId() {
		return aPId;
		}
		public void setaPId(long aPId) {
		this.aPId = aPId;
		}
		public String getAction() {
		return action;
		}
		public void setAction(String action) {
		this.action = action;
		}
		public long getId() {
		return id;
		}
		public void setId(long id) {
		this.id = id;
		}
		public String getAspiration() {
		return aspiration;
		}
		public void setAspiration(String aspiration) {
		this.aspiration = aspiration;
		}
		public long getAspirationId() {
		return aspirationId;
		}
		public void setAspirationId(long aspirationId) {
		this.aspirationId = aspirationId;
		}
		public String getAssetAction() {
		return assetAction;
		}
		public void setAssetAction(String assetAction) {
		this.assetAction = assetAction;
		}
		public long getAssetId() {
		return assetId;
		}
		public void setAssetId(long assetId) {
		this.assetId = assetId;
		}
		public String getAssetRef() {
		return assetRef;
		}
		public void setAssetRef(String assetRef) {
		this.assetRef = assetRef;
		}
		public String getAssetValidate() {
		return assetValidate;
		}
		public void setAssetValidate(String assetValidate) {
		this.assetValidate = assetValidate;
		}
		public String getRef() {
		return ref;
		}
		public void setRef(String ref) {
		this.ref = ref;
		}
		public String getValidate() {
		return validate;
		}
		public void setValidate(String validate) {
		this.validate = validate;
		}
		public long getAssetItemOrder() {
		return assetItemOrder;
		}
		public void setAssetItemOrder(long assetItemOrder) {
		this.assetItemOrder = assetItemOrder;
		}
		public String getAssetItemRef() {
		return assetItemRef;
		}
		public void setAssetItemRef(String assetItemRef) {
		this.assetItemRef = assetItemRef;
		}
		public String getAssetItemName() {
		return assetItemName;
		}
		public void setAssetItemName(String assetItemName) {
		this.assetItemName = assetItemName;
		}
		public String getBaseVehicle() {
		return baseVehicle;
		}
		public void setBaseVehicle(String baseVehicle) {
		this.baseVehicle = baseVehicle;
		}
		public long getBaseVehicleId() {
		return baseVehicleId;
		}
		public void setBaseVehicleId(long baseVehicleId) {
		this.baseVehicleId = baseVehicleId;
		}
		public long getBedLengthId() {
		return bedLengthId;
		}
		public void setBedLengthId(long bedLengthId) {
		this.bedLengthId = bedLengthId;
		}
		public long getBedTypeId() {
		return bedTypeId;
		}
		public void setBedTypeId(long bedTypeId) {
		this.bedTypeId = bedTypeId;
		}
		public long getBodyNumDoorsId() {
		return bodyNumDoorsId;
		}
		public void setBodyNumDoorsId(long bodyNumDoorsId) {
		this.bodyNumDoorsId = bodyNumDoorsId;
		}
		public long getBodyTypeId() {
		return bodyTypeId;
		}
		public void setBodyTypeId(long bodyTypeId) {
		this.bodyTypeId = bodyTypeId;
		}
		public long getBrakeABSId() {
		return brakeABSId;
		}
		public void setBrakeABSId(long brakeABSId) {
		this.brakeABSId = brakeABSId;
		}
		public long getBrakeSystemId() {
		return brakeSystemId;
		}
		public void setBrakeSystemId(long brakeSystemId) {
		this.brakeSystemId = brakeSystemId;
		}
		public long getCylinderHeadTypeId() {
		return cylinderHeadTypeId;
		}
		public void setCylinderHeadTypeId(long cylinderHeadTypeId) {
		this.cylinderHeadTypeId = cylinderHeadTypeId;
		}
		public long getDisplayOrder() {
		return displayOrder;
		}
		public void setDisplayOrder(long displayOrder) {
		this.displayOrder = displayOrder;
		}
		public long getDriveTypeId() {
		return driveTypeId;
		}
		public void setDriveTypeId(long driveTypeId) {
		this.driveTypeId = driveTypeId;
		}
		public String getEngineBase() {
		return engineBase;
		}
		public void setEngineBase(String engineBase) {
		this.engineBase = engineBase;
		}
		public long getEngineBaseId() {
		return engineBaseId;
		}
		public void setEngineBaseId(long engineBaseId) {
		this.engineBaseId = engineBaseId;
		}
		public String getEngineDesignation() {
		return engineDesignation;
		}
		public void setEngineDesignation(String engineDesignation) {
		this.engineDesignation = engineDesignation;
		}
		public long getEngineDesignationId() {
		return engineDesignationId;
		}
		public void setEngineDesignationId(long engineDesignationId) {
		this.engineDesignationId = engineDesignationId;
		}
		public long getEngineMfrId() {
		return engineMfrId;
		}
		public void setEngineMfrId(long engineMfrId) {
		this.engineMfrId = engineMfrId;
		}
		public String getEngineVersion() {
		return engineVersion;
		}
		public void setEngineVersion(String engineVersion) {
		this.engineVersion = engineVersion;
		}
		public long getEngineVersionId() {
		return engineVersionId;
		}
		public void setEngineVersionId(long engineVersionId) {
		this.engineVersionId = engineVersionId;
		}
		public String getEngineVIN() {
		return engineVIN;
		}
		public void setEngineVIN(String engineVIN) {
		this.engineVIN = engineVIN;
		}
		public long getEngineVINId() {
		return engineVINId;
		}
		public void setEngineVINId(long engineVINId) {
		this.engineVINId = engineVINId;
		}
		public long getFrontBrakeTypeId() {
		return frontBrakeTypeId;
		}
		public void setFrontBrakeTypeId(long frontBrakeTypeId) {
		this.frontBrakeTypeId = frontBrakeTypeId;
		}
		public long getFrontSpringTypeId() {
		return frontSpringTypeId;
		}
		public void setFrontSpringTypeId(long frontSpringTypeId) {
		this.frontSpringTypeId = frontSpringTypeId;
		}
		public long getFuelDeliverySubTypeId() {
		return fuelDeliverySubTypeId;
		}
		public void setFuelDeliverySubTypeId(long fuelDeliverySubTypeId) {
		this.fuelDeliverySubTypeId = fuelDeliverySubTypeId;
		}
		public long getFuelDeliveryTypeId() {
		return fuelDeliveryTypeId;
		}
		public void setFuelDeliveryTypeId(long fuelDeliveryTypeId) {
		this.fuelDeliveryTypeId = fuelDeliveryTypeId;
		}
		public long getFuelSystemControlTypeId() {
		return fuelSystemControlTypeId;
		}
		public void setFuelSystemControlTypeId(long fuelSystemControlTypeId) {
		this.fuelSystemControlTypeId = fuelSystemControlTypeId;
		}
		public long getFuelSystemDesignId() {
		return fuelSystemDesignId;
		}
		public void setFuelSystemDesignId(long fuelSystemDesignId) {
		this.fuelSystemDesignId = fuelSystemDesignId;
		}
		public long getFuelTypeId() {
		return fuelTypeId;
		}
		public void setFuelTypeId(long fuelTypeId) {
		this.fuelTypeId = fuelTypeId;
		}
		public long getIgnitionSystemTypeId() {
		return ignitionSystemTypeId;
		}
		public void setIgnitionSystemTypeId(long ignitionSystemTypeId) {
		this.ignitionSystemTypeId = ignitionSystemTypeId;
		}
		public long getMakeId() {
		return makeId;
		}
		public void setMakeId(long makeId) {
		this.makeId = makeId;
		}
		public String getMfrLabel() {
		return mfrLabel;
		}
		public void setMfrLabel(String mfrLabel) {
		this.mfrLabel = mfrLabel;
		}
		public long getMfrBodyCodeId() {
		return mfrBodyCodeId;
		}
		public void setMfrBodyCodeId(long mfrBodyCodeId) {
		this.mfrBodyCodeId = mfrBodyCodeId;
		}
		public long getModelId() {
		return modelId;
		}
		public void setModelId(long modelId) {
		this.modelId = modelId;
		}
		public String getNote() {
		return note;
		}
		public void setNote(String note) {
		this.note = note;
		}
		public long getNoteId() {
		return noteId;
		}
		public void setNoteId(long noteId) {
		this.noteId = noteId;
		}
		public String getNoteLang() {
		return noteLang;
		}
		public void setNoteLang(String noteLang) {
		this.noteLang = noteLang;
		}
		public String getPart() {
		return part;
		}
		public void setPart(String part) {
		this.part = part;
		}
		public String getPartBrandAAIAId() {
		return partBrandAAIAId;
		}
		public void setPartBrandAAIAId(String partBrandAAIAId) {
		this.partBrandAAIAId = partBrandAAIAId;
		}
		public String getPartType() {
		return partType;
		}
		public void setPartType(String partType) {
		this.partType = partType;
		}
		public long getPartTypeId() {
		return partTypeId;
		}
		public void setPartTypeId(long partTypeId) {
		this.partTypeId = partTypeId;
		}
		public String getPosition() {
		return position;
		}
		public void setPosition(String position) {
		this.position = position;
		}
		public long getPositionId() {
		return positionId;
		}
		public void setPositionId(long positionId) {
		this.positionId = positionId;
		}
		public long getPowerOutputId() {
		return powerOutputId;
		}
		public void setPowerOutputId(long powerOutputId) {
		this.powerOutputId = powerOutputId;
		}
		public long getQualId() {
		return qualId;
		}
		public void setQualId(long qualId) {
		this.qualId = qualId;
		}
		public String getqParamUom() {
		return qParamUom;
		}
		public void setqParamUom(String qParamUom) {
		this.qParamUom = qParamUom;
		}
		public String getqParamValue() {
		return qParamValue;
		}
		public void setqParamValue(String qParamValue) {
		this.qParamValue = qParamValue;
		}
		public String getqParamAltValue() {
		return qParamAltValue;
		}
		public void setqParamAltValue(String qParamAltValue) {
		this.qParamAltValue = qParamAltValue;
		}
		public String getqParamAltUom() {
		return qParamAltUom;
		}
		public void setqParamAltUom(String qParamAltUom) {
		this.qParamAltUom = qParamAltUom;
		}
		public String getqPText() {
		return qPText;
		}
		public void setqPText(String qPText) {
		this.qPText = qPText;
		}
		public long getQty() {
		return qty;
		}
		public void setQty(long qty) {
		this.qty = qty;
		}
		public long getRearBrakeTypeId() {
		return rearBrakeTypeId;
		}
		public void setRearBrakeTypeId(long rearBrakeTypeId) {
		this.rearBrakeTypeId = rearBrakeTypeId;
		}
		public long getRearSpringTypeId() {
		return rearSpringTypeId;
		}
		public void setRearSpringTypeId(long rearSpringTypeId) {
		this.rearSpringTypeId = rearSpringTypeId;
		}
		public long getRegionId() {
		return regionId;
		}
		public void setRegionId(long regionId) {
		this.regionId = regionId;
		}
		public long getSteeringTypeId() {
		return steeringTypeId;
		}
		public void setSteeringTypeId(long steeringTypeId) {
		this.steeringTypeId = steeringTypeId;
		}
		public long getSteeringSystemId() {
		return steeringSystemId;
		}
		public void setSteeringSystemId(long steeringSystemId) {
		this.steeringSystemId = steeringSystemId;
		}
		public String getSubModel() {
		return subModel;
		}
		public void setSubModel(String subModel) {
		this.subModel = subModel;
		}
		public long getSubModelId() {
		return subModelId;
		}
		public void setSubModelId(long subModelId) {
		this.subModelId = subModelId;
		}
		public long getTransElecContolledId() {
		return transElecContolledId;
		}
		public void setTransElecContolledId(long transElecContolledId) {
		this.transElecContolledId = transElecContolledId;
		}
		public long getTransmissionMfrId() {
		return transmissionMfrId;
		}
		public void setTransmissionMfrId(long transmissionMfrId) {
		this.transmissionMfrId = transmissionMfrId;
		}
		public long getTransmissionMfrCodeId() {
		return transmissionMfrCodeId;
		}
		public void setTransmissionMfrCodeId(long transmissionMfrCodeId) {
		this.transmissionMfrCodeId = transmissionMfrCodeId;
		}
		public long getTransmissionBaseId() {
		return transmissionBaseId;
		}
		public void setTransmissionBaseId(long transmissionBaseId) {
		this.transmissionBaseId = transmissionBaseId;
		}
		public long getTransmissionControlTypeId() {
		return transmissionControlTypeId;
		}
		public void setTransmissionControlTypeId(long transmissionControlTypeId) {
		this.transmissionControlTypeId = transmissionControlTypeId;
		}
		public long getTransmissionNumSpeedsId() {
		return transmissionNumSpeedsId;
		}
		public void setTransmissionNumSpeedsId(long transmissionNumSpeedsId) {
		this.transmissionNumSpeedsId = transmissionNumSpeedsId;
		}
		public long getTransmissionTypeId() {
		return transmissionTypeId;
		}
		public void setTransmissionTypeId(long transmissionTypeId) {
		this.transmissionTypeId = transmissionTypeId;
		}
		public long getValvesPerEngineId() {
		return valvesPerEngineId;
		}
		public void setValvesPerEngineId(long valvesPerEngineId) {
		this.valvesPerEngineId = valvesPerEngineId;
		}
		public long getVehicleTypeId() {
		return vehicleTypeId;
		}
		public void setVehicleTypeId(long vehicleTypeId) {
		this.vehicleTypeId = vehicleTypeId;
		}
		public long getWheelBaseId() {
		return wheelBaseId;
		}
		public void setWheelBaseId(long wheelBaseId) {
		this.wheelBaseId = wheelBaseId;
		}
		public String getYearsFrom() {
		return yearsFrom;
		}
		public void setYearsFrom(String yearsFrom) {
		this.yearsFrom = yearsFrom;
		}
		public String getYearsTo() {
		return yearsTo;
		}
		public void setYearsTo(String yearsTo) {
		this.yearsTo = yearsTo;
		}
		public String getDriveType() {
		return driveType;
		}
		public void setDriveType(String driveType) {
		this.driveType = driveType;
		}
		@Override
		public String toString() {
		return "App [aPId=" + aPId + ", action=" + action + ", id=" + id
		+ ", aspiration=" + aspiration + ", aspirationId="
		+ aspirationId + ", assetAction=" + assetAction + ", assetId="
		+ assetId + ", assetRef=" + assetRef + ", assetValidate="
		+ assetValidate + ", ref=" + ref + ", validate=" + validate
		+ ", assetItemOrder=" + assetItemOrder + ", assetItemRef="
		+ assetItemRef + ", assetItemName=" + assetItemName
		+ ", baseVehicle=" + baseVehicle + ", baseVehicleId="
		+ baseVehicleId + ", bedLengthId=" + bedLengthId
		+ ", bedTypeId=" + bedTypeId + ", bodyNumDoorsId="
		+ bodyNumDoorsId + ", bodyTypeId=" + bodyTypeId
		+ ", brakeABSId=" + brakeABSId + ", brakeSystemId="
		+ brakeSystemId + ", cylinderHeadTypeId=" + cylinderHeadTypeId
		+ ", displayOrder=" + displayOrder + ", driveTypeId="
		+ driveTypeId + ", engineBase=" + engineBase
		+ ", engineBaseId=" + engineBaseId + ", engineDesignation="
		+ engineDesignation + ", engineDesignationId="
		+ engineDesignationId + ", engineMfrId=" + engineMfrId
		+ ", engineVersion=" + engineVersion + ", engineVersionId="
		+ engineVersionId + ", engineVIN=" + engineVIN
		+ ", engineVINId=" + engineVINId + ", frontBrakeTypeId="
		+ frontBrakeTypeId + ", frontSpringTypeId=" + frontSpringTypeId
		+ ", fuelDeliverySubTypeId=" + fuelDeliverySubTypeId
		+ ", fuelDeliveryTypeId=" + fuelDeliveryTypeId
		+ ", fuelSystemControlTypeId=" + fuelSystemControlTypeId
		+ ", fuelSystemDesignId=" + fuelSystemDesignId
		+ ", fuelTypeId=" + fuelTypeId + ", ignitionSystemTypeId="
		+ ignitionSystemTypeId + ", makeId=" + makeId + ", mfrLabel="
		+ mfrLabel + ", mfrBodyCodeId=" + mfrBodyCodeId + ", modelId="
		+ modelId + ", note=" + note + ", noteId=" + noteId
		+ ", noteLang=" + noteLang + ", part=" + part
		+ ", partBrandAAIAId=" + partBrandAAIAId + ", partType="
		+ partType + ", partTypeId=" + partTypeId + ", position="
		+ position + ", positionId=" + positionId + ", powerOutputId="
		+ powerOutputId + ", qualId=" + qualId + ", qParamUom="
		+ qParamUom + ", qParamValue=" + qParamValue
		+ ", qParamAltValue=" + qParamAltValue + ", qParamAltUom="
		+ qParamAltUom + ", qPText=" + qPText + ", qty=" + qty
		+ ", rearBrakeTypeId=" + rearBrakeTypeId
		+ ", rearSpringTypeId=" + rearSpringTypeId + ", regionId="
		+ regionId + ", steeringTypeId=" + steeringTypeId
		+ ", steeringSystemId=" + steeringSystemId + ", subModel="
		+ subModel + ", subModelId=" + subModelId
		+ ", transElecContolledId=" + transElecContolledId
		+ ", transmissionMfrId=" + transmissionMfrId
		+ ", transmissionMfrCodeId=" + transmissionMfrCodeId
		+ ", transmissionBaseId=" + transmissionBaseId
		+ ", transmissionControlTypeId=" + transmissionControlTypeId
		+ ", transmissionNumSpeedsId=" + transmissionNumSpeedsId
		+ ", transmissionTypeId=" + transmissionTypeId
		+ ", valvesPerEngineId=" + valvesPerEngineId
		+ ", vehicleTypeId=" + vehicleTypeId + ", wheelBaseId="
		+ wheelBaseId + ", yearsFrom=" + yearsFrom + ", yearsTo="
		+ yearsTo + ", version=" + driveType + "]";
		}
}






