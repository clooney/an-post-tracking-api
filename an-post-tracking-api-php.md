An Post Tracking API - PHP
================================
Use PHP to track An Post shipments with An Post Tracking API.

Features
--------
- Real-time An Post tracking.
- Batch An Post tracking.
- Other features to manage your An Post tracking.

Installation
------------

Installation is easy:

    $ composer require trackingmore/trackingmore-sdk-php

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your An Post shipments.

Usage
----------

Create a tracking (Real-time tracking):

      require('vendor/autoload.php');

      use Trackingmore\TrackingMoreException;
      use TrackingMore\Trackings;
        
      $key = 'your api key';
      $response = null;
      $trackings = new Trackings($key);
      
      try {
        $params = ['tracking_number'=>'CP730500199GB','courier_code'=>'an-post'];
        $response = $trackings->createTracking($params);
      } catch (TrackingMoreException $e) {
        echo $e->getMessage();
      }

      print_r($response);

Create trackings (Max. 40 tracking numbers create in one call):

        require('vendor/autoload.php');

        use Trackingmore\TrackingMoreException;
        use TrackingMore\Trackings;
        
        $key = 'your api key';
        $response = null;
        $trackings = new Trackings($key);
        
        try {
            $params = [
                ['tracking_number'=>'RF054985422GB','courier_code'=>'an-post'],
                ['tracking_number'=>'LO366992772GB','courier_code'=>'an-post']
            ];
            $response = $trackings->batchCreateTrackings($params);
        } catch (TrackingMoreException $e) {
            echo $e->getMessage();
        }
        
        print_r($response);


Get status of the shipment:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['courier_code'=>'an-post','created_date_min'=>'2023-08-23T06:00:00+00:00','created_date_max'=>'2023-09-05T07:20:42+00:00'];
        $response = $trackings->getTrackingResults($params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);


Update a tracking by ID:

    require('vendor/autoload.php');

    use Trackingmore\TrackingMoreException;
    use TrackingMore\Trackings;
    
    $key = 'your api key';
    $response = null;
    $trackings = new Trackings($key);
    
    try {
        $params = ['customer_name'=>'New name','note'=>'New tests order note'];
        $idString = '9bcffe4c7caf66b47430d8e262518152';
        $response = $trackings->updateTrackingByID($idString,$params);
    } catch (TrackingMoreException $e) {
        echo $e->getMessage();
    }
    
    print_r($response);
